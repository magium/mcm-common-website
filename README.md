# Magium Configuration Manager Common Website Configuration Options

This is used in conjunction with the [Magium Configuration Manager](https://github.com/magium/configuration-manager).  It provides some basic configuration options that most websites will use to provides some level of customization.  This could include things like website titles, copyright dates, and such.  On its own, these configuration options do not make much sense to have a component like this, but when used within the context of the Magium Configuration Manager it means that all of these configuration options can be managed via a UI or CLI on the production system without having to do a deployment to change configuration options.

# Installation
`composer install magium/mcm-common-website`

This will also install `magium/configuration-manager` if it has not been installed in your project yet.

# Usage

First you need to configure the Magium Configuration Manager.  You will find this information on its GitHub link above or on this [YouTube video](https://www.youtube.com/watch?v=76MLD9Kl2Lk).

You can use the `bin/magium-configuration` CLI to manage the settings OR you can use the UI.  The UI, however, is intended to be run from within your application because it uses the same configuration mechanisms that your application would use if it were using the MCM.  However, if you want to just test out the system there is a [standalone script that you can use for testing](https://github.com/magium/configuration-manager/tree/develop/tests/View/standalone).

Your application may have different ways of wiring dependency injection and such, but if you have the MCM all wired up you would do something like this:

```
<?php
require_once 'vendor/autoload.php';

$factory = new \Magium\Configuration\MagiumConfigurationFactory();
$config = $factory->getManager()->getConfiguration();

?>
<html>
    <head>
        <title><?php echo htmlspecialchars(
            $config->getValue(Magium\Mcm\Common\Website\Constants::GENERAL_TITLE)
        ); ?></title>
    </head>
    <body>
    <h1><a
        href="<?php echo htmlspecialchars(
            $config->getValue(Magium\Mcm\Common\Website\Constants::URL_BASE)
        ); ?>">
        <?php echo htmlspecialchars(
            $config->getValue(Magium\Mcm\Common\Website\Constants::GENERAL_TITLE)
        ); ?></a>
        <div>Some content</div>
        <footer>
            <span>Copyright
                <span><?php
                    echo htmlspecialchars(
                        $config->getValue(Magium\Mcm\Common\Website\Constants::COPYRIGHT_DATE)
                    ); ?></span>
                <span><?php
                    echo htmlspecialchars(
                    $config->getValue(Magium\Mcm\Common\Website\Constants::COPYRIGHT_OWNER)
                ); ?></span>
        </footer>
    </body>
</html>
```

