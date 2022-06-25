---
title: YOLO V3 Implementation with Pytorch & Change Language
summary: YOLO V3- dictionary translation! (字典转换！)
tags:
- Deep Learning
date: "2019-06-20T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Photo by aitube.io
  focal_point: Smart

links:
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
---

<h2>source code</h2>
This link behind shows how to implement <a href="https://blog.paperspace.com/how-to-implement-a-yolo-object-detector-in-pytorch/">YOLOv3 with pytorch instructions</a>
In my tutorial, I give a solution to convert Label to Chinese Character.

<h2>4 Steps To Convert Label to Chinese</h2>

<h3>1. Change coconame</h3>
<p> First of all, we need to translate english label to chinese label
<a href="https://github.com/hanqingguo/YoloV3Pytorch/blob/master/data/coco.names">translated labels is availiable here</a></p>
<h3>2. Use FreeType to write a script to draw chinese characters</h3>
<br>
<p> Because Opencv doesn't support chinese character, we need to use a known font style to draw chinese character, it contains 3 parts:
  <ol>
<li><code>draw_ft_bitmap(self, img, bitmap, pen, color)</code><br>
draw each char <br>
<pre>
    :param bitmap: bitmap
    :param pen:    pen
    :param color:  pen color e.g.(0,0,255) - red
    :return:       image
</pre>
 </li>
<li><code>draw_string(self, img, x_pos, y_pos, text, color)</code><br>
  draw string <br>
<pre>
    :param x_pos: text x-postion on img
    :param y_pos: text y-postion on img
    :param text:  text (unicode)
    :param color: text color
    :return:      image
</pre>
</li>

<li><code>draw_text(self, image, pos, text, text_size, text_color)</code><br>
  (draw chinese(or not) text with ttf <br>
<pre>
    :param image:     image(numpy.ndarray) to draw text
    :param pos:       where to draw text
    :param text:      the context, for chinese should be unicode type
    :param text_size: text size
    :param text_color:text color
    :return:          image
</pre>
</li>
</ol>
</p>

<h3>3. Download msyh.ttf</h3>
<p> .ttf file is dependency to specify font style, it would be loaded in FreeType script, click <a href="https://github.com/hanqingguo/YoloV3Pytorch/blob/master/msyh.ttf">here</a> to Download </p>

<h3>4. Apply ft2 Chinese Character to yolo</h3>
<p>In main detect flow (cam_detect.py), instead of using <code>cv2.imshow()</code>, we use <code>ft.draw_text()</code></p>
<p>
   comment <code>cv2.putText</code> part, use <code>ft.draw_text</code> instead <br>
<pre>
    # c2 = c1[0] + t_size[0] + 3, c1[1] + t_size[1] + 4
    # cv2.rectangle(img, c1, c2,color, -1)
    # cv2.rectangle(img, c1, c2, color, -1)
    # cv2.putText(img, label, (c1[0], c1[1] + t_size[1] + 4), cv2.FONT_HERSHEY_PLAIN, 2, [225,255,255], 1);
    ft = ft2.put_chinese_text('msyh.ttf')
    ft.draw_text(image=img, pos=(c1[0], c1[1] + t_size[1] - 7), text=label, text_size=15, text_color=[255, 255, 255])
</pre></p>
<h3>Before Translate</h3>
<video width="400" controls>
<source src="eng_caption.mp4" type="video/mp4">
</video>
<br/>
<h3>After Translate</h3>
<video width="400" controls>
<source src="cn_caption.mp4" type="video/mp4">
</video>
</br>
<p>You can Download All source code from my github,<a href="https://github.com/hanqingguo/YoloV3Pytorch">here</a>
</p>
