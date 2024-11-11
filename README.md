
# New feature on ezwayi
example: news

A brief description of what this project does and who it's for




note: OSFYW = "or similar feature you want to copy)


1: duplicate themes/ezwayi/layout/search(OSFYW)  and renamed it "news"

2: duplicate source/search.php(OSFYW)  and renamed it "news.php". 
	In news.php
 
  
        $wo['title'] = "News" . ' | ' . $wo['config']['siteTitle'];
        $wo['content'] = Wo_LoadPage('search/content');

3: In Ajax.php duplicatie ->

         case 'search':
            include('sources/search.php');
            break;
to -> both for pro and non pro condition (2 times)

         case 'news':
                include('sources/news.php');
                break;

4: Same for the index.php

5: in .htaccess duplicate

        RewriteRule ^search(/?|)$ index.php?link1=search [NC,QSA]
        RewriteRule ^search/([^\/]+)(\/|)$ index.php?link1=search&query=$1 [NC,QSA]

and edit this to 

        RewriteRule ^news(/?|)$ index.php?link1=news [NC,QSA]
        RewriteRule ^news/([^\/]+)(\/|)$ index.php?link1=news&query=$1 [NC,QSA]

6: in function_general.php -> Wo_SeoLink function duplicate:

         '/^index\.php\?link1=search&query=(.*)$/i',
to 

         '/^index\.php\?link1=news&query=(.*)$/i',

and  duplicate

        $config['site_url'] . '/search/$1',

to

        $config['site_url'] . '/news/$1',

7: Feature's location is:

            <a href="<?php echo Wo_SeoLink('index.php?link1=news'); ?>" data-ajax="?link1=news">news</a>
