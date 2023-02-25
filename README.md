 # How to create an Magento 2 Plugin
 An example of how to create a basic Magento 2 plugin for sorting the post list in the Magento admin area. Here are the steps you can follow:
## Let us start
- Create a new module for your plugin. You can create a new directory for your module under the app/code directory in your Magento installation. For example, you might create a directory called MyCompany_PostSort.
- Inside the module directory, create a registration.php file with the following code:

```php
<?php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'MyCompany_PostSort',
    __DIR__
);
```
 -- > This code registers your module with Magento.

- Create a etc/module.xml file in your module directory with the following code:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="MyCompany_PostSort" setup_version="1.0.0" />
</config>
```
This code defines the name and version of your module.

Create a etc/di.xml file in your module directory with the following code:
```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Backend\Block\Widget\Grid">
        <plugin name="mycompany_postsort" type="MyCompany\PostSort\Plugin\Backend\Block\Widget\Grid" sortOrder="10" disabled="false" />
    </type>
</config>
```
--> This code configures a plugin for the Magento\Backend\Block\Widget\Grid class. The plugin is defined in a new PHP file that you will create in the next step.

- Create a new PHP file at the following location: MyCompany/PostSort/Plugin/Backend/Block/Widget/Grid.php. The file should contain the following code:
``` php
<?php
namespace MyCompany\PostSort\Plugin\Backend\Block\Widget;
class Grid
{
    public function beforeSetCollection(\Magento\Backend\Block\Widget\Grid $subject, $collection)
    {
        $collection->setOrder('post_id', 'DESC');
    }
}
``` 
--> This code defines a plugin for the setCollection method of the Magento\Backend\Block\Widget\Grid class. The plugin sorts the post list in the Magento admin area by the post ID in descending order.

Install and enable your module. You can do this by running the following command from your Magento root directory:
``` python
php bin/magento setup:upgrade
```
After following these steps, your Magento 2 plugin should be active and the post list in the Magento admin area should be sorted by post ID in descending order. You can modify the plugin code and configuration as needed to customize the sorting behavior or add other functionality to your plugin.
