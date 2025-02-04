### Reproducible Example of Embedding Packages and Variables from Previous Pages in a Quarto Book

#### Overview
In Notebook2, I use the {{< embed Notebook1.qmd#import-packages echo=true >}} directive to embed a code cell from Notebook1.
The expectation is that the code from Notebook1 will be executed in Notebook2, making the imported libraries and variables available for use.

#### Actual Behavior
The embedded code from Notebook1 is not automatically executed in Notebook2.
Since the imports from Notebook1 are not executed in Notebook2, the libraries (e.g., pandas as pd) and variables defined in Notebook1 are not available when you try to use them in Notebook2.

### Exemple
#### Notebook1
````quarto
```{python}
# | echo: true
# | label: import-packages

import pandas as pd
import altair as alt
import seaborn as sns
from matplotlib import pyplot as plt

penguins = sns.load_dataset("penguins")

```

```{python}
# | label: species-counts
penguins.groupby("species").size().reset_index(name="count")
```
````

#### Notebook2
````quarto

{{< embed Notebook1.qmd#import-packages echo=true >}}

```{python}
# | echo: true

penguins.head()

# Perform some analysis
penguins.describe()

```
````
