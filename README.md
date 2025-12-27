
## Working papers

{% assign working_papers = site.data.papers | where_exp: "paper", "paper.journal_status != 'published'" %}
{% for paper in working_papers %}
* **{{ paper.title }}**{% if paper.coauthors %} (with {{ paper.coauthors | join: ", " }}){% endif %}
    {% if paper.journal_status %}
    - *{{ paper.journal_status }}*
    {% endif %}
  - <a href="#" id="toggle-link-{{ forloop.index }}" onclick="toggleAbstract('abstract-{{ forloop.index }}', 'toggle-link-{{ forloop.index }}'); return false;">Show Abstract</a><br>
  <span id="abstract-{{ forloop.index }}" style="display:none;">{{ paper.abstract }}</span>
  {% if paper.links %}
  - {% for link in paper.links %}<a href="{{ link.url }}" target="_blank">{{ link.name }}</a>{% if forloop.last == false %}, {% endif %}{% endfor %}
  {% endif %}
{% endfor %}

## Publications

{% assign published_papers = site.data.papers | where: "journal_status", "published" %}
{% for paper in published_papers %}
* **{{ paper.title }}**{% if paper.coauthors %} (with {{ paper.coauthors | join: ", " }}){% endif %}
    {% if paper.journal %}
    - *{{ paper.journal }}{% if paper.year %}, {{ paper.year }}{% endif %}*
    {% endif %}
  - <a href="#" id="toggle-link-pub-{{ forloop.index }}" onclick="toggleAbstract('abstract-pub-{{ forloop.index }}', 'toggle-link-pub-{{ forloop.index }}'); return false;">Show Abstract</a><br>
  <span id="abstract-pub-{{ forloop.index }}" style="display:none;">{{ paper.abstract }}</span>
  {% if paper.links %}
  - {% for link in paper.links %}<a href="{{ link.url }}" target="_blank">{{ link.name }}</a>{% if forloop.last == false %}, {% endif %}{% endfor %}
  {% endif %}
{% endfor %}

<script>
function toggleAbstract(abstractId, linkId) {
  var el = document.getElementById(abstractId);
  var link = document.getElementById(linkId);
  if (el.style.display === 'none') {
    el.style.display = 'block';
    link.textContent = 'Hide Abstract';
  } else {
    el.style.display = 'none';
    link.textContent = 'Show Abstract';
  }
}
</script>


{% if site.data.wip and site.data.wip.size > 0 %}
## Work in progress
{% for wip in site.data.wip %}
* **{{ wip.title }}**{% if wip.coauthors %} (with {{ wip.coauthors | join: ", " }}){% endif %}
{% endfor %}
{% endif %}

## CV
You can find my CV <a href="CV_MW.pdf">here</a>.
