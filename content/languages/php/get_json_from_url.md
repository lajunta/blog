---
title: "Get Json From Url"
date: 2021-04-09T11:55:26+08:00
draft: false
---

```php
<?php

get_header();

$url = "http://10.2.110.120:8080/wp-json/cyberbuf/news";

$json = file_get_contents($url);

$news = json_decode($json);

?>
<?php

get_header();

$url = "http://10.2.110.120:8080/wp-json/cyberbuf/news";

$json = file_get_contents($url);

$news = json_decode($json);

?>

<section>
    <div class="container pb-5 mb-5">

        <?php foreach($news as $n){     ?>
          <h1 class="my-5"><?php echo $n->title; ?></h1>
          <p ><?php echo $n->category; ?></p>
          <p ><?php echo $n->description; ?></p>
          <img src=<?php echo $n->image ?>  alt="">
        <?php } ?>
        
      </div>
</section>


<?php get_footer(); ?>

<section>
        <div class="container pb-5 mb-5">

                <?php foreach($news as $n){     ?>

                <h1 class="my-5"><?php echo $n->title; ?></h1>
                <p ><?php echo $n->category; ?></p>
                <p ><?php echo $n->description; ?></p>
                <img src=<?php echo $n->image ?>  alt="">

                <?php } ?>

        </div>
</section>


<?php get_footer(); ?>

```