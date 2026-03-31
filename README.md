## 👋 Hellooooooo! Costantino here... 😃 


Geoscientist (PhD) working on GIS, remote sensing, and spatial modeling.

## 🔬 Current projects

<table>
  <tr>
    <td>
      <a href="https://github.com/constantineshovel/inue">
        <img src="https://raw.githubusercontent.com/constantineshovel/inue/main/inueabout.png" width="50" />
      </a>
    </td>
    <td><strong><a href="https://github.com/constantineshovel/inue">INUE</a></strong> → postfire erosion susceptibility mapping</td>
  </tr>
  <tr>
    <td>
      <a href="https://github.com/constantineshovel/SUBSTR8">
        <img src="https://raw.githubusercontent.com/constantineshovel/SUBSTR8/main/SUBSTRAT8%20logo.png" width="50" />
      </a>
    </td>
    <td><strong><a href="https://github.com/constantineshovel/SUBSTR8">SUBSTR8</a></strong> → modular framework for spatial analysis</td>
  </tr>
</table>



## 🧰 Tools & methods
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![QGIS](https://img.shields.io/badge/QGIS-589632?style=for-the-badge&logo=qgis&logoColor=white)](https://qgis.org)
[![ArcGIS](https://img.shields.io/badge/ArcGIS-E0302F?style=for-the-badge&logo=arcgis&logoColor=white)](https://www.esri.com)
[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.org)

 

## 📌 Focus
I use data and code to help communities face climate change, especially post-fire risk ✨ 

## 📚 Recent Publications
name: Update ORCID Publications

on:
  schedule:
    - cron: "0 0 * * 1" # Ogni lunedì alle 00:00
  workflow_dispatch: # Permette l'avvio manuale immediato

jobs:
  update-orcid:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Fetch and Update README
        shell: python
        run: |
          import urllib.request, json, re
          
          ORCID_ID = "0009-0001-3968-0395"
          URL = f"https://pub.orcid.org/v3.0/{ORCID_ID}/works"
          
          try:
              req = urllib.request.Request(URL, headers={"Accept": "application/json"})
              with urllib.request.urlopen(req) as response:
                  data = json.loads(response.read().decode())
              
              lines = []
              # Prende le ultime 5 pubblicazioni
              for group in data.get('group', [])[:5]:
                  summary = group.get('work-summary', [{}])[0]
                  title = summary.get('title', {}).get('title', {}).get('value', 'Titolo non disponibile')
                  pub_date = summary.get('publication-date')
                  year = pub_date.get('year', {}).get('value', 'N/A') if pub_date else 'N/A'
                  lines.append(f"- **{title}** ({year})")
              
              content = "\n".join(lines) if lines else "Nessuna pubblicazione trovata."
              
              with open("README.md", "r", encoding="utf-8") as f:
                  readme = f.read()
              
              # Sostituzione del contenuto tra i tag
              new_readme = re.sub(
                  r".*", 
                  f"\n{content}\n", 
                  readme, 
                  flags=re.DOTALL
              )
              
              with open("README.md", "w", encoding="utf-8") as f:
                  f.write(new_readme)
                  
          except Exception as e:
              print(f"Errore durante l'aggiornamento: {e}")
              exit(1)

      - name: Commit and Push
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"
          git add README.md
          git commit -m "Update ORCID publications" || exit 0
          git push


## 📫 Contact
- Email: costantino.pala.geo@proton.me
- ORCID: https://orcid.org/0009-0001-3968-0395


## 🍸 Fun fact
Geoscientist by day, elegant cat by night.


<img src="https://komarev.com/ghpvc/?username=constantineshovel&color=blueviolet&style=flat-square" alt="Visitor's Count" />
<!--
**constantineshovel/constantineshovel** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
