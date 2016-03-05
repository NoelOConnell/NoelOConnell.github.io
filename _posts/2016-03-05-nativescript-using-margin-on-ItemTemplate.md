---
layout: post
permalink: /2016-03-05-nativescript-using-margin-on-ItemTemplate/
title: Getting margin to work on ItemTemplate with Android
path: 2016-03-05-nativescript-using-margin-on-ItemTemplate.md
---

Recently while developing a NativeScript Android app, I wanted to create a card style ListView with a margin between each row to give it that kinda material design look.
Since NativeScript uses <a href="https://docs.nativescript.org/ui/styling">CSS</a> for it's styling, I presumed adding margin to each item in the list would do the trick.

{% highlight XML %}
<list-view items="{{ jobList }}" id="jobList" row="1" colSpan="2" separatorColor="transparent">
    <list-view.itemTemplate>
        <stack-layout>
            <grid-layout columns="*, auto" rows="auto, auto" class="list-item">
                <Label row="0" text="{{ name }}" class="list-title" />
                <Label row="1" text="{{ location }}" class="list-subtitle" />
                <Label col="1" text="{{ status }}" class="{{'tag-sm status-' + statusClass}}" />
            </grid-layout>
        </stack-layout>
    </list-view.itemTemplate>
</list-view>

{% endhighlight %}