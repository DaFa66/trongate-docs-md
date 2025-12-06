# Using Packagist With Trongate


This guide outlines the process for integrating third-party PHP libraries into Trongate applications using 
    [Packagist](https://packagist.org/), the primary repository for Composer packages. 
    For demonstration purposes, the instructions below specifically focus on downloading and utilizing 
    [Guzzle](https://packagist.org/packages/guzzlehttp/guzzle), a third-party PHP 
    library that facilitates the sending and receiving of HTTP requests and responses.

### System Requirements


Ensure that the system meets the following requirements:


- **PHP:** PHP 8 or newer is required to use the latest version of Trongate with Packagist.
- **Composer:** Composer must be installed on the system for managing library dependencies. 
        If Composer is not installed, visit 
        [getcomposer.org](https://getcomposer.org/) to download and install it.
    
- **Internet Connection:** An active internet connection is necessary to download packages from Packagist.

### Step 1: Setting Up the Project with Composer


1. **Initialize Composer:** If a `composer.json` file is not already present in the 
        project, create one by running the following command in the project directory:
```
composer init
```


        Follow the prompts to configure the project. This setup helps manage project dependencies.
    
2. **Install Guzzle:** Add Guzzle to the project by running:
```
composer require guzzlehttp/guzzle
```


        This command instructs Composer to find Guzzle on Packagist and install it along with any necessary dependencies.
    
3. **Verify Installation:** Ensure that the Guzzle library has been added to the project by checking 
        that the `composer.json` file includes Guzzle and that the `vendor` directory has been 
        created with Guzzle files in it.
    

### Step 2: Using Guzzle in a Trongate Application


1. **Autoload Dependencies:** To use Guzzle, include Composer's autoloader in the PHP script. 
        Add the following line at the top of the PHP file:
```php
require_once APPPATH.'vendor/autoload.php';
```


        This inclusion ensures that all dependencies, including Guzzle, are loaded and available for use.
    
2. **Create an HTTP Client:** Instantiate a new Guzzle client to make HTTP requests:
```php
$client = new GuzzleHttp\Client();
```


3. **Make an HTTP Request:** Use the client to send a request and retrieve the response:
```php
$response = $client->request('GET', 'https://api.example.com/data');
echo $response->getBody();
```



## Complete Example


Below is an example of using Guzzle within a Trongate controller file to fetch data from GitHub's API:

```php
&lt;?php
require_once APPPATH.'vendor/autoload.php';

use GuzzleHttp\Client;

class Welcome extends Trongate {

    function fetch() {

        $client = new Client();
        try {
            // Fetch repository details, for Trongate, from GitHub API
            $target_url = 'https://api.github.com/repos/trongate/trongate-framework';
            $response = $client->request('GET', $target_url);
            $data = json_decode($response->getBody(), true);

            // Accessing the 'stargazers_count' to get the number of stars
            echo "The Trongate framework has ".$data['stargazers_count']." stars on GitHub.";
        } catch (GuzzleHttp\Exception\GuzzleException $e) {
            echo 'Request failed: '.$e->getMessage();
        }

    }

}
```

> [!TIP]
> **Best Practices**
>
> In the example above, the `APPPATH` constant is used to specify the location of the 
>         `autoload.php` file. All Trongate controllers, view files, and templates have access to the 
>         `APPPATH` constant, which references the application's root directory. This provides a reliable 
>         method for specifying file paths.
> 
> 
> The example also utilizes PHP's `require_once` function, ensuring that the file is included only 
>         once, safeguarding the application's stability.


## Conclusion


Although Trongate has its own 
    [code-sharing platform](https://trongate.io/module-market), there may be instances 
    where downloading third-party code via Packagist is desirable. Packagist offers a vast repository of PHP libraries 
    and packages that can significantly accelerate development and bring advanced functionality to projects with minimal effort.


However, the use of Packagist is not without challenges. Relying on Packagist can lead to potential issues with 
    stability, versioning, and dependencies. Moreover, developers considering using code from Packagist should be aware 
    of potential 
    [security vulnerabilities](https://news.google.com/search?q=Packagist) associated with Packagist.


The Trongate framework enables developers to selectively use Packagist for specific modules, providing precise 
    integration without compromising the overall performance of the application. This targeted approach ensures that 
    enhancements can be made where necessary without affecting the efficiency of the entire system.

