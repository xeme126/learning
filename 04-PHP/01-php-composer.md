# composer install #


# composer config #


# composer usage #

npm install localtunnel -g
npm install localtunnel -g --registry=https://registry.npm.taobao.org

项目配置
mkdir demo && cd demo && echo "{}" > composer.json
composer config repo.packagist composer https://packagist.phpcomposer.com

全局配置
composer config -g repo.packagist compser https://pcakagist.phpcomposer.com
php /usr/bin/composer config -g repo.packagist composer https://packagist.phpcomposer.com

php /usr/bin/composer global require "fxp/composer-asset-plugin:.2.0"
php /usr/bin/composer create-project yiisoft/yii2-app-basic basic ~2.0
php /usr/bin/composer create-project yiisoft/yii2-app-advanced advanced ~2.0

