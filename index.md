---
title: Home
layout: default
nav_exclude: false
nav_order: 1
---

{% assign variables = site.data[site.data_folder].variables %}
{% assign course_calendar = site.data[site.data_folder].course_calendar %}
{% assign offset_week = 1 %}

{: .text-grey-dk-200 .pt-4 .lh-0 }
# Data Management  

{: .text-grey-dk-300 .fw-300 }
## MSBA 504 - University San Diego - Professor Chris Young

{{ variables.term }}
{: .md-badge-purple }

{: .warning .fs-50 }
🚧 🚧 This site is under construction preparing for the Fall semester 🚧 🚧

## Course Calendar

{% assign first_date = course_calendar[0].date | date: '%s' %}
{% assign first_day = course_calendar[0].date | date: '%w' %}
{% assign prev_week_no = offset_week %}
<table style="table-layout: fixed; text-align: left; width: 100%;">
    <colspan>
        <col style="width: 20%;">
        <col style="width: 20%; border: none">
        <col style="width: 60%; border: none">
    </colspan>
    <thead>
        <tr class="header">
            <th colspan="3" style="padding-left:8%; font-size-adjust:0.75"> Week {{ offset_week }} </th>
        </tr>
    </thead>
    <tbody>
{% for row in course_calendar %}
    {% assign week_no = row.date | date: '%s' | minus: first_date | divided_by: 60 | divided_by: 60 | divided_by: 24 | plus: first_day | minus: 1 | divided_by: 7 | plus: offset_week %}
    <!-- Week number is calculated as follows. Take the current row date as epoch and subtract the first date from course calendar.
    Convert it to number of days (How many days ahead is the current row date from first date) and add the day number of the first day of the week.
    Sunday is considered as 0, Monday as 1 and so on (strftime), but to start our week from Monday, we subtract 1 and then divide by 7 to get week no
    Offset week is used since fall quarter starts in Week 0 while other quarters start in Week 1 -->
    {% if week_no != prev_week_no %}
    </tbody>
</table>
<table style="table-layout: fixed; text-align: left; width: 100%;">
    <colspan>
        <col style="width: 20%;">
        <col style="width: 20%; border: none">
        <col style="width: 60%; border: none">
    </colspan>
    <thead>
        <tr class="header">
            <th colspan="3" style="padding-left:8%; font-size-adjust:0.75"> Week {{ week_no }} </th>
        </tr>
    </thead>
    <tbody>
    {% endif %}
    {% assign prev_week_no = week_no %}
        <tr>
            <td style="text-align: center"> {{ row.date | date: "%a, %b %d" }} </td>
            <td style="text-align: center">
              {% if row.label == "LECT" %} <span class="md-cal-badge md-cal-badge-blue"> {{ row.label }} </span>
              {% elsif row.label == "LAB" %} <span class="md-cal-badge md-cal-badge-purple"> {{ row.label }} </span>
              {% elsif row.label == "CNCL" %} <span class="md-cal-badge md-cal-badge-red"> {{ row.label }} </span>
              {% elsif row.label == "ASSG" %} <span class="md-cal-badge md-cal-badge-green"> {{ row.label }} </span>
              {% elsif row.label == "EXAM" %} <span class="md-cal-badge md-cal-badge-gray"> {{ row.label }} </span>
              {% elsif row.label == "QUIZ" %} <span class="md-cal-badge md-cal-badge-green"> {{ row.label }} </span>
              {% elsif row.label == "DEMO" %} <span class="md-cal-badge md-cal-badge-yellow"> {{ row.label }} </span>
              {% else %}
                {% if row.label %} <span class="md-cal-badge md-cal-badge-black"> {{ row.label }} </span>
                {% endif %}
              {% endif %}
            </td>
            <td style="padding-left: 4%">
            {% assign links = row.link | split: ";" %}
            {% if links and links.size != 0 %}
            {% assign titles = row.title | split: ";" %}
            {% for link in links %}
              {% if link and link != '' %} <a href="{{ link }}"> {{ titles[forloop.index0] }} </a> {% unless forloop.last %} <br/> {% endunless %}
              {% else %} {{ titles[forloop.index0] }} {% unless forloop.last %} <br/> {% endunless %}
              {% endif %}
            {% endfor %}
            {% else %} {{ row.title }}
            {% endif %}
            </td>
        </tr>
{% endfor %}
    </tbody>
</table>


