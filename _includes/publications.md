<h2 id="publications" style="margin: 2px 0px -1px;">Research Papers <temp style="font-size:15px;">[</temp><a href="https://scholar.google.com/citations?user=zDviHvcAAAAJ&hl=zh-TW&oi=ao/" target="_blank" style="font-size:15px;">Google Scholar</a><temp style="font-size:15px;">]
</temp></h2>

<div class="publications">
<ol class="bibliography">

{% for link in site.data.publications.main %}

<li>
<div class="pub-row">
  <div class="col-sm-9" style="position: relative;padding-right: 1px;padding-left: 2px;">
      <div class="title"><a href="{{ link.page }}">{{ link.title }}</a></div>
      <div class="author">{{ link.authors }}</div>
      <div class="periodical">{{ link.conference }}
      </div>
    <div class="links">
      {% if link.bibtex %}
        <button type="button"
        class="paper-btn"
        onclick="toggleBib('{{ forloop.index }}', '{{ link.bibtex | relative_url }}')"
        style="font-size:12px;">
        bib
        </button>
      {% endif %}
      {% if link.abstract %}
          <button type="button"
          class="paper-btn"
          onclick="toggleAbstract('{{ forloop.index }}', '{{ link.abstract | relative_url }}')">
            abstract
          </button>
      {% endif %} 
      {% if link.pdf %}
          <button type="button"
          class="paper-btn"
          onclick="window.open('{{ link.pdf }}', '_blank')">
            pdf
          </button>
      {% endif %}
      {% if link.arxiv %}
            <button type="button"
            class="paper-btn"
            onclick="window.open('{{ link.arxiv }}', '_blank')">
            arXiv
            </button>
      {% endif %}
      {% if link.code %}
        <button type="button"
                class="paper-btn"
                onclick="window.open('{{ link.code }}', '_blank')">
          code
        </button>
      {% endif %}
      {% if link.preview %}
        <button type="button"
                class="paper-btn"
                onclick="window.open('{{ link.preview }}', '_blank')">
          preview
        </button>
      {% endif %}
      {% if link.notes %}
        <strong>
          <i style="color:rgb(167, 32, 56);font-size:16px">
            {{ link.notes }}
          </i>
        </strong>
      {% endif %}
      {% if link.others %}
        {{ link.others }}
      {% endif %}
    </div>
    {% if link.bibtex %}
      <div id="bib-{{ forloop.index }}" class="bibtex-content"></div>
    {% endif %}
    {% if link.abstract %}
      <div id="abstract-{{ forloop.index }}" class="abstract-content"></div>
    {% endif %}
  </div>
</div>
</li>

{% endfor %}

</ol>
</div>

<script>
function toggleBib(id, url) {
  var bib = document.getElementById("bib-" + id);

  if (bib.style.display === "block") {
    bib.style.display = "none";
    return;
  }

  if (bib.innerHTML.trim() === "") {
    fetch(url)
      .then(response => {
        if (!response.ok) {
          throw new Error("Could not load BibTeX.");
        }
        return response.text();
      })
      .then(text => {
        var pre = document.createElement("pre");
        pre.textContent = text;
        bib.appendChild(pre);
        bib.style.display = "block";
      })
      .catch(error => {
        bib.textContent = "Unable to load BibTeX.";
        bib.style.display = "block";
        console.error(error);
      });
  } else {
    bib.style.display = "block";
  }
}
</script>

<script>
function toggleAbstract(id, url) {
  var abstract = document.getElementById("abstract-" + id);

  if (abstract.style.display === "block") {
    abstract.style.display = "none";
    return;
  }

  if (abstract.innerHTML.trim() === "") {
    fetch(url)
      .then(response => {
        if (!response.ok) {
          throw new Error("Could not load abstract.");
        }
        return response.text();
      })
      .then(text => {
        abstract.textContent = text;
        abstract.style.display = "block";
      })
      .catch(error => {
        abstract.textContent = "Unable to load abstract.";
        abstract.style.display = "block";
        console.error(error);
      });
  } else {
    abstract.style.display = "block";
  }
}
</script>