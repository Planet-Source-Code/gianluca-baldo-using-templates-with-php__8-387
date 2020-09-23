<div align="center">

## Using templates with PHP


</div>

### Description

The article explains a personal and simple approach to the use of templates in PHP scripts.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Gianluca Baldo](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/gianluca-baldo.md)
**Level**          |Intermediate
**User Rating**    |3.4 (17 globes from 5 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Coding Standards](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/coding-standards__8-33.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/gianluca-baldo-using-templates-with-php__8-387/archive/master.zip)





### Source Code

```
<P><font face="Verdana, Arial, Helvetica, sans-serif" size="3"><b>Using
 templates with PHP</b></font></P>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">We will assume
 you are planning to develop a PHP application.<BR>
 First question: <I>what are templates</I>?<BR>
 <BR>
 Templates are text files usually containing HTML code and "some tags"
 to fill the HTML with dinamically generated content. Mantaining your
 PHP code separated from the files responsable for the visual part of your
 site, will give the ability to change your site's look & feel in a
 simple and fast way in the future, without having to touch you PHP code.</FONT></P>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">Embedding
 HTML in your PHP is not a good idea. The more you keep your HTML independent
 the easier it will be to maintain you site.<BR>
 An approach like the following, having a PHP file which outputs the HTML
 tags (we assume you have to output the content of the variable $test):<BR>
 </FONT></P>
 <CITE>
<?
 echo "<HTML>
 <HEAD></HEAD>
 <BODY>
 [some HTML here]
 $test
 [some more HTML]<BR> </BODY><BR> </HTML>";
?> </CITE>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">is not convenient
 since changes to your HTML will require that you edit your PHP code. This
 approach can be somehow confusing and not confortable.<BR>
 A better solution could be:</FONT><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">
 </FONT></P>
 <CITE>
 <HTML>
 <HEAD></HEAD>
 <BODY>
 [you HTML here]<BR> <? echo $test; ?><BR> [some more HTML]
 </BODY><BR> </HTML>
</CITE>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">which is
 not a template yet, but we are beginning to separate the HTML tags from
 PHP code.<BR>
 If you need to perform some actions before your <FONT face="Courier New, Courier, mono"><?
 echo $test; ?></FONT> to give the variable $test the correct value
 (i.e. accessing a database table and reading a column value) you'll have
 to add the necessary PHP code, for example at the very top of the file.
 Something like:</FONT><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">
 </FONT></P>
 <CITE><?
 // We assume your are running MySQL
 $query = "SELECT myvalue FROM test_table";<BR> $result = mysql_query($query);<BR> $test = mysql_result($result,0,"myvalue");
?>
 <HTML>
 <HEAD></HEAD>
 <BODY>
 [you HTML here]<BR> <? echo $test; ?><BR> [some more HTML]
 </BODY><BR> </HTML>
</CITE>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">So we now
 have a unique PHP file where we intend to keep HTML tags and PHP code
 separated. This is simpler to mantain and will be clearer to any other
 who will have to edit and/or mantain your script. <BR>
 HTML tools like Dreamweaver can recognize PHP tags and will not alter
 your PHP code. I use to develop PHP applications where the visual part
 is rather complex and Dreamweaver is a good tool to help in the production
 process. <BR>
 So if your WYSIWYG HTML editor do not alter PHP code, you can open your
 script and just make the necessary changes to the HTML. The PHP will be
 generally shown as an icon and you can simply move the code behind that
 icon (if necessary) moving the icon itself.<BR>
 <BR>
 This sounds good enough, so: <I>why should you use templates</I>?<BR>
 Let's see how templates works (well, the way I use templates) and this
 will probably answer the question.<BR>
 <BR>
 First let's create the tamplate file (i.e. sample_template.html). It will
 contain HTML tags we need to create the visual part of our script.<BR>
 </FONT></P>
 <CITE>
 <HTML>
 <HEAD>
 </HEAD>
 <BODY>
 [you HTML here]<BR>
 </BODY>
 </HTML>
</CITE>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">After that,
 let's create the PHP file which will contain the PHP code we need:</FONT></P>
 <CITE><?
 // We assume your are running MySQL
 $query = "SELECT myvalue FROM test_table";<BR> $result = mysql_query($query);<BR> $test = mysql_result($result,0,"myvalue");
 include "<FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">sample_template.html</FONT>";
?>
</CITE>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">We now need
 to make the last change to our HTML file:</FONT></P>
 <CITE> <HTML>
 <HEAD></HEAD>
 <BODY>
 [you HTML here]
 <? echo $test; ?><BR> </BODY><BR> </HTML>
</CITE>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">What we basically
 did is to separate the PHP code and the HTML in two different files. The
 PHP script file performs the necessary actions and, once done, includes
 the template (HTML) file.<BR>
 This is really better than the "one-file" solution since the
 HTML is clear and even graphic designers can open the template files and
 make visual changes to them, being sure they will not accidentally alter
 the PHP behind it.</FONT></P>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2">There are
 many approaches to the templates idea, the one I presented here is the
 one I found more confortable after using some of them. <BR>
 Here are some reference if you want to read something more about templates.</FONT></P>
 <P><FONT face="Verdana, Arial, Helvetica, sans-serif" size="2"><A href="http://www.phpbuilder.com/columns/sascha19990316.php3" target="_blank">Templates
 - why and how to use them in PHP3</A> <FONT size="1">(by Sasha Shumann)</FONT><BR>
 <A href="http://www.phpbuilder.com/columns/david20000512.php3" target="_blank">Templates,
 The PHPLIB Way</A> <FONT size="1">(by David Orr )</FONT><BR>
 <A href="http://www.1perlstreet.com/xq/ASP/txtCodeId.314/lngWId.8/qx/vb/scripts/ShowCode.htm" target="_blank">Using
 Templates</A> <FONT size="1">(by Todd Williams)</FONT><BR>
 <A href="http://www.spilth.org/php/templates/" target="_blank">Includes
 and Templates with PHP</A><BR>
 <BR></FONT></P>
```

