---
title: Members
permalink: /team/members/
---

{% assign role_order = "Postdoc,Grad,Undergrad" | split: "," %}
{% assign role_labels = "Postdoc,Graduate Students,Undergraduate Students" | split: "," %}
{% assign listed = site.team | where_exp: "m", "m.listed != false" %}
{% assign non_alumni = listed | where_exp: "m", "m.role != 'Alumni'" %}
{% assign current = non_alumni | where_exp: "m", "m.role != 'PI'" %}
{% assign alumni  = listed | where: "role", "Alumni" %}

<section class="team-section">
  <h2 class="section-title">Current Members</h2>
  {% for role in role_order %}
    {% assign in_role = current | where: "role", role | sort: "order" %}
    {% if in_role.size > 0 %}
      <section class="team-role">
        <h3 class="team-role-title">{{ role_labels[forloop.index0] }}</h3>
        <div class="team-grid">
          {% for member in in_role %}
            {% include team-card.html member=member %}
          {% endfor %}
        </div>
      </section>
    {% endif %}
  {% endfor %}
</section>

{% if alumni.size > 0 %}
<section class="team-section">
  <h2 class="section-title">Alumni</h2>
  <ul class="alumni-list">
    {% assign alumni_sorted = alumni | sort: "order" %}
    {% for member in alumni_sorted %}
      <li class="alumni-item">
        <span class="alumni-name">{{ member.name }}</span>{% if member.title %} <span class="alumni-sep">·</span> <span class="alumni-title">{{ member.title }}</span>{% endif %}
      </li>
    {% endfor %}
  </ul>
</section>
{% endif %}
