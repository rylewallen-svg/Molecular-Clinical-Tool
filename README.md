# Molecular-Clinical-Tool
Molecular signaling pathway tool to identify the signaling cascade and effects  from drugs or pathologies

<div style="display: flex; flex-direction: column; align-items: center;">
  <h1>Clinical Pathway Tool</h1>
  <h2>NF-κB Pathway Map</h2>
  <h>_________________________________________ </h>


    <!-- Add your pathway image -->
  <img src= alt="NFκB pathway" usemap="#pi3kmap" style="max-width: 90%; height: auto;">
  
    <h>_________________________________________ </h>
  
  <label for="condition">Select a condition:</label><br>
  <select id="condition">
    <option value="colorectal">Stage 3 Colorectal Cancer</option>
  </select>
  <button onclick="analyze()">Analyze</button>
  <div id="output" class="result"></div>

  <script>
    const data = {
      "colorectal": {
        name: "Stage 3 Colorectal Cancer",
        pathways: {
          "PI3K/AKT/mTOR": {
            status: "Upregulated",
            drugs: [
              "Alpelisib (PI3K inhibitor)",
              "Everolimus (mTOR inhibitor)"
            ],
            notes: "PI3K pathway promotes growth and survival of cancer cells."
          },
          "NF-κB → COX-2": {
            status: "Upregulated",
            drugs: [
              "NSAIDs (COX‑2 inhibitors)",
              "Corticosteroids"
            ],
            notes: "NSAIDs inhibit COX-2 but may upregulate IL‑8, which can worsen inflammation and coagulopathy.",
            warnings: [
              "⚠️ IL‑8 upregulation may increase hypercoagulability.",
              "Consider thromboprophylaxis in surgical patients."
            ]
          }
        }
      }
    };

    function analyze() {
      const condition = document.getElementById("condition").value;
      const conditionData = data[condition];
      let output = `<h2>🧾 Condition: ${conditionData.name}</h2>`;
      for (let [pathway, details] of Object.entries(conditionData.pathways)) {
        output += `
          <div class="pathway">
            <h3>🧪 ${pathway}</h3>
            <p>Status: <strong>${details.status}</strong></p>
            <p>${details.notes}</p>
            <p>💊 Drugs: <span class="drug">${details.drugs.join(", ")}</span></p>
        `;
        if (details.warnings) {
          details.warnings.forEach(warning => {
            output += `<p class="warning">${warning}</p>`;
          });
        }
        output += `</div>`;
      }
      document.getElementById("output").innerHTML = output;
    }

    function showInfo(gene) {
      // Basic info for genes
      const geneInfo = {
        "MDM2": "MDM2 is a negative regulator of p53. If MDM2 is inhibited or removed → p53 remains active.",
        "p53": "p53 is a tumor suppressor. When active, causes cell cycle arrest or apoptosis."
        // add more gene-specific info here
      };
      alert(gene + ": " + (geneInfo[gene] || "No info available"));
    }
  </script>
</body>
</html>
