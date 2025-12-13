# Polling With Trongate MX


Polling in Trongate MX allows you to periodically fetch updates from the server, keeping your web application's content fresh without user interaction. Ideal for real-time updates or live data feeds, polling can be controlled declaratively with attributes or programmatically via JavaScript.

## Basic Usage


Use the `mx-trigger` attribute to start polling automatically when the page loads.

### Basic Example:

```html
<div mx-get="api/live_data" mx-trigger="every 5s">
  <!-- Content updates every 5 seconds -->
</div>
```


This fetches data from `api/live_data` every 5 seconds and updates the content.

## Polling Options


Trongate MX offers flexible polling options:


| Option | Description | Example Syntax |
| ---|---|---|
| Basic Polling | Polls at a regular interval immediately. | `mx-trigger="every 10s"` |
| Load Polling | Polls after an initial delay, then repeats. | `mx-trigger="load delay:3s"` |
| Polling with Initial Delay | Delays the first poll, then uses a different interval. | `mx-trigger="load delay:2s, every 7s"` |

## Time Intervals


Specify intervals using these units:


- `s`: seconds
- `m`: minutes
- `h`: hours
- `d`: days

### Examples:

#### Every 3 Seconds:

```html
<div mx-get="api/updates" mx-trigger="every 3s"></div>
```


Fetches updates every 3 seconds.

#### Delayed Start:

```html
<div mx-get="api/data" mx-trigger="load delay:5m"></div>
```


Waits 5 minutes, then polls every 5 minutes.

#### Custom Delay and Interval:

```html
<div mx-get="api/stats" mx-trigger="load delay:1h, every 30m"></div>
```


Waits 1 hour, then polls every 30 minutes.

## Programmatic Polling


You can control polling dynamically with JavaScript using the `TrongateMX` API.

### Starting and Stopping Polling:

```html
<div id="poll-area" mx-get="api/dynamic_data">
  <button onclick="startPoll()">Start Polling</button>
  <button onclick="stopPoll()">Stop Polling</button>
</div>

<script>
function startPoll() {
  const el = document.querySelector('#poll-area');
  if (window.TrongateMX.startPolling(el, '10s')) {
    console.log('Polling started!');
  }
}

function stopPoll() {
  const el = document.querySelector('#poll-area');
  if (window.TrongateMX.stopPolling(el)) {
    console.log('Polling stopped!');
  }
}
</script>
```

### Preventing Automatic Triggering:


Use `mx-trigger="none"` to prevent an element from responding to clicks while still allowing programmatic polling:

```html
<div id="content-area" 
     mx-get="api/fetch_content" 
     mx-trigger="none" 
     mx-after-swap="logUpdate">
  <div>
    <p>This container has content that will be updated through polling.</p>
    <button onclick="beginPolling()">Start Polling</button>
  </div>
</div>

<script>
function logUpdate() {
  console.log('Content updated at: ' + new Date().toLocaleTimeString());
}

function beginPolling() {
  const el = document.querySelector('#content-area');
  if (window.TrongateMX.startPolling(el, '5s')) {
    console.log('Polling started!');
  }
}
</script>
```


This pattern is especially useful for containers with clickable elements inside them or when you want complete control over when polling begins.

## Advanced Example


Toggle polling based on user actions:

```html
<div id="area-1">
  <button mx-post="api/start" mx-target="#response" mx-after-swap="revealArea2">Start</button>
  <div id="response"></div>
</div>

<div id="area-2" style="display: none;" mx-get="api/updates" mx-target="#updates">
  <div id="updates"></div>
  <button onclick="stopPoll()">Stop Polling</button>
</div>

<script>
function revealArea2() {
  document.querySelector('#area-1').remove();
  const areaTwo = document.querySelector('#area-2');
  areaTwo.style.display = 'block';
  window.TrongateMX.startPolling(areaTwo, '5s');
}
function stopPoll() {
  const areaTwo = document.querySelector('#area-2');
  window.TrongateMX.stopPolling(areaTwo);
}
</script>
```


Clicking "Start" triggers a POST, reveals `#area-2`, and begins polling every 5 seconds. "Stop Polling" halts it.

## Polling with Out-of-Band Swaps


Trongate MX can update multiple parts of your page with a single polling request.  This is achieved by combining polling with out-of-band swaps and `mx-target="none"`:

```html
<div id="dashboard-stats" 
     mx-get="dashboard/stats" 
     mx-target="none" 
     mx-trigger="none"
     mx-select-oob='[
       {"select":".current-users","target":"#user-count"},
       {"select":".server-load","target":"#load-meter"},
       {"select":".error-count","target":"#error-panel"}
     ]'>
  <!-- Using mx-trigger="none" prevents clicks from triggering updates -->
  <button onclick="startDashboardPolling()">Activate Live Updates</button>
</div>

<div class="dashboard-widgets">
  <div id="user-count">-- users</div>
  <div id="load-meter">--%</div>
  <div id="error-panel">-- errors</div>
</div>

<script>
function startDashboardPolling() {
  const statsElement = document.querySelector('#dashboard-stats');
  window.TrongateMX.startPolling(statsElement, '5s');
  this.innerHTML = "Live Updates Active";
  this.disabled = true;
}
</script>
```


With this setup:


- The main container has `mx-target="none"` so it won't be updated directly
- `mx-trigger="none"` prevents accidental triggering when clicking the container
- The API endpoint returns fragments that match the selectors in `mx-select-oob`:

```html
<!-- Example API response from dashboard/stats -->
<div class="current-users">254 active users</div>
<div class="server-load">42%</div>
<div class="error-count">0 errors in last hour</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Documentation pertaining to out of band swaps is available from [here](../0030Swapping_Content/0060out_of_band_swaps.md).


## Polling State


Elements actively polling have a `data-polling-active="true"` attribute, which is removed when polling stops.  This provides an opportunity to apply CSS styling to elements that are currently being targetted by polling.  For example:

```css
[data-polling-active] {
  border: 2px solid green;
}
```

> [!TIP]
> **Best Practices**
>
> #### Best Practices
> 
> 
> - **Server Load**: Use reasonable intervals (5+ seconds) to avoid overloading your server.
> - **Prevent Accidental Triggers**: Use `mx-trigger="none"` when you only want programmatic polling.
> - **Dynamic Control**: Use `startPolling` and `stopPolling` for runtime flexibility.
> - **Error Handling**: Check return values (`true`/`false`) from polling methods.
> - **Cleanup**: Polling stops automatically when elements are removed from the DOM.


> [!NOTE]
> **Just To Let You Know...**
>
> #### Technical Notes
> 
> 
> - Declarative polling (`mx-trigger="every Xs"`) applies only to elements present on page load.
> - Programmatic polling works anytime, even on dynamically added elements.
> - Polling avoids `mx-post` to prevent unintended form submissions.
> - Use `TrongateMX.stopAllPolling()` to halt all polling globally.


## Summary


Trongate MX's polling combines simple attribute-based updates with powerful JavaScript control, making it easy to build dynamic, real-time web applications.

