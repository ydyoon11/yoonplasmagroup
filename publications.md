---
title: Publications
permalink: /publications/
---

{% assign submitted_by_status = site.publications | where: "status", "submitted" %}
{% assign submitted_by_journal = site.publications | where: "journal", "manuscript submitted" %}
{% assign submitted = submitted_by_status | concat: submitted_by_journal | uniq | sort: "date" | reverse %}
{% assign published = site.publications | where_exp: "pub", "pub.status != 'submitted'" | where_exp: "pub", "pub.journal != 'manuscript submitted'" %}
{% assign by_year = published | sort: "date" | reverse | group_by: "year" %}
{% assign by_year_sorted = by_year | sort: "name" | reverse %}

{% if site.publications.size == 0 %}
<p class="muted">No publications listed yet.</p>
{% endif %}

{% if submitted.size > 0 %}
  <section class="pub-year-section" id="submitted">
    <h2 class="pub-year">Submitted</h2>
    <ul class="pub-list">
      {% for pub in submitted %}
        {% include publication-item.html pub=pub %}
      {% endfor %}
    </ul>
  </section>
{% endif %}

{% for year_group in by_year_sorted %}
  <section class="pub-year-section">
    <h2 class="pub-year">{{ year_group.name }}</h2>
    <ul class="pub-list">
      {% for pub in year_group.items %}
        {% include publication-item.html pub=pub %}
      {% endfor %}
    </ul>
  </section>
{% endfor %}
