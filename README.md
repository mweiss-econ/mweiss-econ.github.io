
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
  - {% for link in paper.links %}{% if link.name == 'Cite' %}<a href="#" onclick="loadCitePopup('{{ link.url }}'); return false;">Cite</a>{% else %}<a href="{{ link.url }}" target="_blank">{{ link.name }}</a>{% endif %}{% if forloop.last == false %}, {% endif %}{% endfor %}
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

function loadCitePopup(filePath) {
  fetch('CitationFiles/' + filePath)
    .then(response => response.text())
    .then(content => {
      showCiteModal(content);
    })
    .catch(error => {
      alert('Error loading citation: ' + error);
    });
}

function showCiteModal(content) {
  var modal = document.createElement('div');
  modal.id = 'citeModal';
  modal.style.cssText = 'position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.5); display: flex; align-items: center; justify-content: center; z-index: 1000;';
  
  var modalContent = document.createElement('div');
  modalContent.style.cssText = 'background-color: white; padding: 30px; border-radius: 8px; max-width: 800px; width: 90%; max-height: 80vh; overflow-y: auto; box-shadow: 0 4px 6px rgba(0,0,0,0.1);';
  
  var closeBtn = document.createElement('button');
  closeBtn.textContent = '✕';
  closeBtn.style.cssText = 'float: right; background: none; border: none; font-size: 24px; cursor: pointer; color: #666;';
  closeBtn.onclick = function() { document.body.removeChild(modal); };
  
  var preElement = document.createElement('pre');
  preElement.style.cssText = 'font-family: monospace; white-space: pre-wrap; word-wrap: break-word; font-size: 14px; background-color: #f5f5f5; padding: 15px; border-radius: 4px;';
  preElement.innerHTML = content;
  
  var copyBtn = document.createElement('button');
  copyBtn.textContent = 'Copy to Clipboard';
  copyBtn.style.cssText = 'padding: 10px 20px; margin-top: 15px; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer;';
  copyBtn.onclick = function() {
    navigator.clipboard.writeText(content);
    copyBtn.textContent = 'Copied!';
    setTimeout(function() { copyBtn.textContent = 'Copy to Clipboard'; }, 2000);
  };
  
  modalContent.appendChild(closeBtn);
  modalContent.appendChild(preElement);
  modalContent.appendChild(copyBtn);
  modal.appendChild(modalContent);
  
  modal.onclick = function(e) {
    if (e.target === modal) {
      document.body.removeChild(modal);
    }
  };
  
  document.body.appendChild(modal);
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
