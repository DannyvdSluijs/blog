---
title: Applying Decorator Pattern In ZendFramework
date: 2017-11-08 21:32:38
layout: post
tags:
---
A big refactoring job at my workplace has led me to review some of the [ViewHelpers](https://docs.zendframework.com/zend-view/helpers/intro/) we are having in one of our core applications.
These helpers where targetting different types of properties resulting in the use of several view helpers for a 
single view and the same view helper being used by multiple (unrelated) views. This results in a high coupling whereas we would like a lower coupling.

In my opinion we have improved by implementing a series of [Decorator Pattern](http://designpatternsphp.readthedocs.io/en/latest/Structural/Decorator/README.html) for the individual entities.
```php
<?php 
#./module/App/src/View/Helper/UserDecorator.php

namespace App\View\Helper;

use Zend\View\Helper\AbstractHelper;

class UserDecorator extends AbstractHelper
{
    /** @var User */
    private $user;

    /**
     * Clone the user decorator with the provided user
     * @param User $user
     * @return UserDecorator
     */
    public function __invoke(User $user)
    {
        $clone = clone $this;
        $clone->user = $user;

        return $clone;
    }
    
    /**
     * Get the full name of the user
     * @return string
     */
    public function getFullName()
    {
        return sprintf(
            '%s %s',
            $this->user->getFirstName(),
            $this->user->getLastName()
        );
    }
}
```

Some plumping needs to be done in order to get the decorator available in the view:
```php
<?php
# ./module/App/config/module.config.php

use App\View\Helper;

return [
  'view_helpers' => [
    'invokables' => [
      'userDecorator' => Helper\UserDecorator::class
    ]	
  ]
];
```

Using it in the view is rather simple:
```php
<?php
#./module/App/view/user/overview.php
$user = $this->userDecorator($this->user);

printf('Full name: %s', $user->getFullName());
```

