# Gépi tanulás a hitelkártya-csalások felderítésére kiegyensúlyozatlan osztályozással
Egy teljes körű gépi tanulási projekt, amely a Kaggle „Credit Card Fraud Detection” (hitelkártya-csalás észlelése) adatkészletét felhasználva elemzi és osztályozza a csalárd hitelkártya-tranzakciókat. A projekt kitér az adatok előfeldolgozására, a súlyos osztálykiegyensúlyozatlanság kezelésére, valamint különféle osztályozó algoritmusok teljesítményének összehasonlítására.

## 📌 A projekt áttekintése

A hitelkártya-csalások felderítése egy klasszikus, nagy téttel bíró, erősen kiegyensúlyozatlan osztályozási feladat:
* **Összes tranzakció:** 284 807
* **Csalárd tranzakciók:** 492 (~0,172%)
* **Jellemzők (attribútumok):** 28 darab, PCA-transzformáción átesett numerikus jellemző (`V1`–`V28`), kiegészítve az időponttal (`Time`), az összeggel (`Amount`) és a célváltozóval (`Class`).

Mivel a szabályos tranzakciók az adatok több mint 99,8%-át teszik ki, az olyan hagyományos mérőszámok, mint a **pontosság (Accuracy)**, félrevezetőek lehetnek (egy naiv modell, amely minden tranzakciót szabályosnak jelöl, 99,8%-os pontosságot ér el, miközben egyetlen csalást sem ismer fel). A projekt során a legfontosabb optimalizálási mérőszámok a **felismerési arány (Recall)**, a **Precision-Recall AUC (PR-AUC)** és az **F1-érték (F1-Score)**.

## 🛠️ Technológiai háttér és módszerek

* **Nyelv:** Python
* **Könyvtárak:** `pandas`, `numpy`, `scikit-learn`, `imbalanced-learn`, `matplotlib`, `seaborn`
* **Kiegyensúlyozatlanság kezelése:** SMOTE (szintetikus kisebbségi túlmintavételezési technika), véletlenszerű alulmintavételezés (Random Under-Sampling) és költségérzékeny tanulás (`class_weight='balanced'`)
* **Vizsgált modellek:**
* Logisztikus regresszió (alapmodell)
* Random Forest (véletlen erdő) osztályozó
* XGBoost / LightGBM

---

## 📊 Főbb eredmények és értékelés

| Modell | Módszer | Precizió (Precision) | Felismerési arány (Recall) | PR-AUC |
| :--- | :--- | :--- | :--- | :--- |
| **Logisztikus regresszió** | Alapmodell | 0,86 | 0,62 | 0,73 |
| **Logisztikus regresszió** | Kiegyensúlyozott súlyok | 0,06 | 0,91 | 0,71 |
| **Random Forest** | SMOTE | 0.88 | 0.82 | 0.85 |
| **Random Forest** | Kiegyensúlyozott súlyok | **0.93** | **0.84** | **0.87** |

> *Tipp: A visszahívási arány (recall) előtérbe helyezésével több csalás azonosítható, bár ezzel együtt nőhet a téves riasztások száma is; ezeket azonban egy második ellenőrzési lépés során szűrhetjük.*

---

## 🚀 Első lépések

### 1. A tárhely (repository) klónozása
```bash
git clone [https://github.com/](https://github.com/)<felhasználóneved>/credit-card-fraud-detection.git
cd credit-card-fraud-detection
