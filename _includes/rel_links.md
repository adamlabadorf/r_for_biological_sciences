{%- for item in site.data.schedule -%}
    {%- assign i = forloop.index0 -%}
    {%- if item.theory_slug == page.slug -%}
        {%- assign type = "theory" -%}
        {%- break -%}
    {%- elsif item.practice_slug == page.slug -%}
        {%- assign type = "practice" -%}
        {%- break -%}
    {%- elsif item.project_slug == page.slug -%}
        {%- assign type = "project" -%}
        {%- break -%}
    {%- endif -%}
{%- endfor -%}

{%- assign curr = site.data.schedule[i] -%}

{%- if i == empty -%}
    Could not find flanking links for {{ page.slug }}
{%- else -%}
    {%- if type == "project" -%}

    {%- else -%}
        {%- if i > 0 -%}
        Previous:
            {%- assign prev_i = i | minus: 1 -%}
            {%- assign prev = site.data.schedule[prev_i] -%}
            {%- if type == "theory" -%}
                {%- assign page = site.theory | where:"slug", prev.theory_slug | first  -%}
<a href="{{ prev.theory_slug }}.html">{{ page.title }}</a>
            {%- else -%}
                {%- assign page = site.practice | where:"slug", prev.practice_slug | first  -%}
<a href="{{ prev.practice_slug }}.html">{{ page.title }}</a>
            {%- endif -%}
&nbsp; | &nbsp;
        {%- endif -%}

        {%- assign next_i = i | plus: 1 -%}
        {%- assign next = site.data.schedule[next_i] -%}
        {%- if next  -%}
        Next: 
            {%- if type == "theory" -%}
                {%- assign page = site.theory | where:"slug", next.theory_slug | first  -%}
<a href="{{ next.theory_slug }}.html">{{ page.title }}</a>
            {%- else -%}
                {%- assign page = site.practice | where:"slug", next.practice_slug | first  -%}
<a href="{{ next.practice_slug }}.html">{{ page.title }}</a>
            {%- endif -%}
        {%- endif -%}

    {%- endif -%}
{%- endif -%}
