---
title: "About"
layout: default
sitemap: false
permalink: /about/
---

{% if site.author %}
	I’m Gabriel, a Data Scientist with a passion for uncovering the stories data holds. My work is fueled by a commitment to using data to tackle critical global issues and advance the [Sustainable Development Goals](https://sdgs.un.org/goals). With a foundation in Applied Mathematics, Operations Research, and Geospatial Analysis, I focus on extracting insights from spatial data to inform policy decisions, support climate adaptation, and foster inclusive development.

	🛰️ Currently, I’m focused on projects that combine satellite imagery, spatial modeling, and data visualization to turn complex data into actionable insights. I’m always learning, staying at the cutting edge of technology to innovate and solve new challenges.

	🌟 I’m eager to connect with others who geek out over geospatial data, sustainability, and innovation. 
	💬 [Let's chat](https://github.com/g4brielvs/g4brielvs/discussions)! Whether it’s about data, linguistics, sci-fi, or New York City, or simply sharing something close to your heart, I'm always happy to swap ideas and stories!
    {% assign author = site.data.authors[site.author] %}
    {{ author.bio }}
{% endif %}
