---
layout: page
title: About
description: 坚持才能更好。越努力越幸运。
keywords: SK
comments: true
menu: 关于
permalink: /about/
---
软件开发。

## 坚信

* 越自律，越自由!

## 联系

* GitHub：[aaronshang](https://github.com/aaronshang)
* Email: aaron.shang@qq.com

## Skill Keywords

#### Software Engineer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_software_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Mobile Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_mobile_app_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>

#### Windows Developer Keywords
<div class="btn-inline">
    {% for keyword in site.skill_windows_keywords %}
    <button class="btn btn-outline" type="button">{{ keyword }}</button>
    {% endfor %}
</div>
