---
extends: _layouts.post
section: content
title: Magento Profiler
date: 2018-11-21
categories: [feature]
description: Debug magento using profiler
---

Debug magento using profiler to see how block are loading and how much are time they are take.

```php
$_SERVER['MAGE_PROFILER'] = 'html';
# at beginning of index.php page
```