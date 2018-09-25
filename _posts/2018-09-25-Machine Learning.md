---
layout: post
title: Sample Post
excerpt: "Just about everything you'll need to style in the theme: headings, paragraphs, blockquotes, tables, code blocks, and more."
categories: [Machine Learning]
comments: true
---

## Machine Learning First Post

처음 테스트용으로 포스팅합니다. 

# 인공지능

## 머신러닝

### 회귀, 분류


### 정의

> 인간의 사고 능력을 모방하여 적용하는 이론

## 솔베이 학회 사진
![file 21-09-2016 1 00 54 pm](https://user-images.githubusercontent.com/26396102/46000665-2de72680-c0e4-11e8-8c0f-86945855df21.jpeg)

## Code Snippets

{% highlight css %}
def variable_summaries(var):
    """텐서에 많은 양의 요약정보(summaries)를 붙인다. (텐서보드 시각화를 위해서)"""
    with tf.name_scope('summaries'):
      mean = tf.reduce_mean(var)
      tf.summary.scalar('mean', mean)
      with tf.name_scope('stddev'):
        stddev = tf.sqrt(tf.reduce_mean(tf.square(var - mean)))
      tf.summary.scalar('stddev', stddev)
      tf.summary.scalar('max', tf.reduce_max(var))
      tf.summary.scalar('min', tf.reduce_min(var))
      tf.summary.histogram('histogram', var)
}
{% endhighlight %}


## Notices

**Watch out!** You can also add notices by appending `{: .notice}` to a paragraph.
{: .notice}
