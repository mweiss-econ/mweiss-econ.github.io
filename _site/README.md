
## Working papers

{% for paper in site.data.papers %}
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
