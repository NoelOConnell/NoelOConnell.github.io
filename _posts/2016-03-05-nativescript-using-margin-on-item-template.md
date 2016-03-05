---
layout: post
permalink: /2016-03-05-nativescript-using-margin-on-item-template/
title: Getting margin to work on item-template with Android
path: 2016-03-05-nativescript-using-margin-on-item-template.md
---

Recently while developing a NativeScript Android app, I wanted to create a card style list-view with a margin between each row to give it that kinda material design look.
Since NativeScript uses <a href="https://docs.nativescript.org/ui/styling">CSS</a> for it's styling, I presumed adding margin to each item in the list would do the trick.

### The problem
Here's my css styling with the margin-bottom on each item in the list. All other css properties took effect just not margin-bottom.

{% highlight css %}
.list-item {
    background-color: white;
    padding: 10;
    margin-bottom: 5;    
}
{% endhighlight %}

{% highlight XML %}
{% raw %}
<list-view items="{{jobList}}" row="1" colSpan="2" separatorColor="transparent">
    <list-view.itemTemplate>
        <!-- .list-item margin-bottom NOT working -->
        <grid-layout columns="*, auto" rows="auto, auto" class="list-item">
            <Label row="0" text="{{ name }}" class="list-title" />
            <Label row="1" text="{{ location }}" class="list-subtitle" />
            <Label col="1" text="{{ status }}" class="{{'tag-sm status-' + statusClass}}" />
        </grid-layout>
    </list-view.itemTemplate>
</list-view>
{% endraw %}
{% endhighlight %}

<img src="/img/posts/margin-not-working.png" style="width: 350px;">

### The solution

After spending sometime scratching my head and trying various solutions I found a fix. By wrapping my grid-layout with a stack-layout margin took effect.
It seems as though margin will not work if it's being applied to the first element after list-view.itemTemplate.

{% highlight XML %}
{% raw %}
<list-view items="{{jobList}}" row="1" colSpan="2" separatorColor="transparent">
    <list-view.itemTemplate>
        <stack-layout>
            <!-- .list-item margin-bottom working after wrapping it with stack-layout -->
            <grid-layout columns="*, auto" rows="auto, auto" class="list-item">
                <Label row="0" text="{{ name }}" class="list-title" />
                <Label row="1" text="{{ location }}" class="list-subtitle" />
                <Label col="1" text="{{ status }}" class="{{'tag-sm status-' + statusClass}}" />
            </grid-layout>
        </stack-layout>
    </list-view.itemTemplate>
</list-view>
{% endraw %}
{% endhighlight %}

<img src="/img/posts/margin-working.png" style="width: 350px;">