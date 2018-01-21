<div class="entry-content">

要对图形进行操作，首先要新建一个画布，通过imagecreatetruecolor函数可以创建一个真彩色的空白图片：
<pre class="code">$img = imagecreatetruecolor(100, 100);</pre>
GD库中对于画笔所用的颜色，需要通过imagecolorallocate函数进行分配，通过参数设定RGB的颜色值来确定画笔的颜色：
<pre class="code">$red = imagecolorallocate($img, 0xFF, 0x00, 0x00);</pre>
然后我们通过调用绘制线段函数imageline进行线条的绘制，通过指定起点跟终点来最终得到线条。
<pre class="code">imageline($img, 0, 0, 100, 100, $red);</pre>
线条绘制好以后，通过header与imagepng进行图像的输出。
<pre class="code">header("content-type: image/png");
imagepng($img);</pre>
最后可以调用imagedestroy释放该图片占用的内存。
<pre class="code">imagedestroy($img);</pre>
通过上面的步骤，可以发现PHP绘制图形非常的简单，但很多时候我们不只是需要输出图片，可能我们还需要得到一个图片文件，可以通过imagepng函数指定文件名将绘制后的图像保存到文件中。
<pre class="code">imagepng($img, 'img.png');</pre>
<h3>给图片添加水印</h3>
<div id="J_CodeDescr" class="code-description">
<div class="code-desc co">

给图片添加水印的方法一般有两种，一种是在图片上面加上一个字符串，另一种是在图片上加上一个logo或者其他的图片。

因为这里处理的是已经存在的图片，所以可以直接从已存在的图片建立画布，通过imagecreatefromjpeg可以直接从图片文件创建图像。
<pre class="code">$im = imagecreatefromjpeg($filename);</pre>
创建图像对象以后，我们就可以通过前面的GD函数，绘制字符串到图像上。如果要加的水印是一个logo图片，那么就需要再建立一个图像对象，然后通过GD函数imagecopy将logo的图像复制到源图像中。
<pre class="code">$logo = imagecreatefrompng($filename);
imagecopy($im, $logo, 15, 15, 0, 0, $width, $height);</pre>
当将logo图片复制到原图片上以后，将加水印后的图片输出保存就完成了加水印处理。
<pre class="code">imagejpeg($im, $filename);</pre>
</div>
</div>
</div>
