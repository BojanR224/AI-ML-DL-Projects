---
jupyter:
  accelerator: GPU
  colab:
    collapsed_sections:
    - Xe0BrSMu8b9D
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

::: {.cell .markdown id="Xe0BrSMu8b9D"}
\#\#Фаза 2 - База на податоци и претпроцесирање
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="BQY2lQjdM5hB" outputId="9617fe36-7920-4a63-bcc8-944cc58a54a4"}
``` {.python}
from google.colab import drive
drive.mount('/content/drive')
```

::: {.output .stream .stdout}
    Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).
:::
:::

::: {.cell .code id="cbniSay2yGhj"}
``` {.python}
import pandas as pd
import numpy as np
```
:::

::: {.cell .code colab="{\"height\":423,\"base_uri\":\"https://localhost:8080/\"}" id="B-H-0i0Izhzb" outputId="942a2366-b72a-49c2-80c5-4fcbf8077486"}
``` {.python}
grade = pd.read_csv('drive/MyDrive/Grade.csv')
grade
```

::: {.output .execute_result execution_count="2"}
```{=html}
  <div id="df-b572f103-b018-4bff-b8af-0351e78d5046">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>patient ID</th>
      <th>grade (GlaS)</th>
      <th>grade (Sirinukunwattana et al. 2015)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>testA_1</td>
      <td>4</td>
      <td>benign</td>
      <td>adenomatous</td>
    </tr>
    <tr>
      <th>1</th>
      <td>testA_10</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>testA_11</td>
      <td>9</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>testA_12</td>
      <td>11</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
    <tr>
      <th>4</th>
      <td>testA_13</td>
      <td>7</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>160</th>
      <td>train_82</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately-to-poorly differentated</td>
    </tr>
    <tr>
      <th>161</th>
      <td>train_83</td>
      <td>11</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
    <tr>
      <th>162</th>
      <td>train_84</td>
      <td>15</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>163</th>
      <td>train_85</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>164</th>
      <td>train_9</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
  </tbody>
</table>
<p>165 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b572f103-b018-4bff-b8af-0351e78d5046')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b572f103-b018-4bff-b8af-0351e78d5046 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b572f103-b018-4bff-b8af-0351e78d5046');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .code id="Gw4c2g8p0QIk"}
``` {.python}
from PIL import Image
```
:::

::: {.cell .code colab="{\"height\":539,\"base_uri\":\"https://localhost:8080/\"}" id="80k20dpQ1DZD" outputId="e1263c46-5017-496d-c184-b2bcfd064236"}
``` {.python}
import glob

file_paths = glob.glob("drive/MyDrive/images/*")
Image.open("drive/MyDrive/images/testA_1.bmp")
```

::: {.output .execute_result execution_count="18"}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/dfe3906da4b1de82cd986e94eb531217b6dc0059.png)
:::
:::

::: {.cell .markdown id="CO1kVAn9EqrW"}
### Одвојување на податоците според името на сликата (препорачано од самата страна од каде ги симнав податоците)
:::

::: {.cell .code id="DcK9aqF646v4"}
``` {.python}
train_data = grade[grade['name'].str.contains('train')]
test_data = grade[grade['name'].str.contains('test')]
```
:::

::: {.cell .code colab="{\"height\":423,\"base_uri\":\"https://localhost:8080/\"}" id="zrvGIOVF7z11" outputId="ec65aa23-9490-4a71-cf0d-2fca0e148ee5"}
``` {.python}
train_data
```

::: {.output .execute_result execution_count="24"}
```{=html}
  <div id="df-fa9a0b5b-a94b-47e2-ba96-a234401aeb15">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>patient ID</th>
      <th>grade (GlaS)</th>
      <th>grade (Sirinukunwattana et al. 2015)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>80</th>
      <td>train_1</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
    </tr>
    <tr>
      <th>81</th>
      <td>train_10</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
    </tr>
    <tr>
      <th>82</th>
      <td>train_11</td>
      <td>10</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
    <tr>
      <th>83</th>
      <td>train_12</td>
      <td>13</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>84</th>
      <td>train_13</td>
      <td>1</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>160</th>
      <td>train_82</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately-to-poorly differentated</td>
    </tr>
    <tr>
      <th>161</th>
      <td>train_83</td>
      <td>11</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
    <tr>
      <th>162</th>
      <td>train_84</td>
      <td>15</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>163</th>
      <td>train_85</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>164</th>
      <td>train_9</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fa9a0b5b-a94b-47e2-ba96-a234401aeb15')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-fa9a0b5b-a94b-47e2-ba96-a234401aeb15 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fa9a0b5b-a94b-47e2-ba96-a234401aeb15');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .code colab="{\"height\":423,\"base_uri\":\"https://localhost:8080/\"}" id="DXBPPSoT8Xim" outputId="66b926ca-7d97-4a9d-c417-705976cfe15b"}
``` {.python}
test_data
```

::: {.output .execute_result execution_count="25"}
```{=html}
  <div id="df-1dfd9311-17cd-4781-98e4-c0c99342c026">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>patient ID</th>
      <th>grade (GlaS)</th>
      <th>grade (Sirinukunwattana et al. 2015)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>testA_1</td>
      <td>4</td>
      <td>benign</td>
      <td>adenomatous</td>
    </tr>
    <tr>
      <th>1</th>
      <td>testA_10</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>2</th>
      <td>testA_11</td>
      <td>9</td>
      <td>benign</td>
      <td>healthy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>testA_12</td>
      <td>11</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
    <tr>
      <th>4</th>
      <td>testA_13</td>
      <td>7</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>75</th>
      <td>testB_5</td>
      <td>5</td>
      <td>benign</td>
      <td>adenomatous</td>
    </tr>
    <tr>
      <th>76</th>
      <td>testB_6</td>
      <td>3</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
    </tr>
    <tr>
      <th>77</th>
      <td>testB_7</td>
      <td>5</td>
      <td>benign</td>
      <td>adenomatous</td>
    </tr>
    <tr>
      <th>78</th>
      <td>testB_8</td>
      <td>7</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
    </tr>
    <tr>
      <th>79</th>
      <td>testB_9</td>
      <td>1</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
    </tr>
  </tbody>
</table>
<p>80 rows × 4 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-1dfd9311-17cd-4781-98e4-c0c99342c026')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-1dfd9311-17cd-4781-98e4-c0c99342c026 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-1dfd9311-17cd-4781-98e4-c0c99342c026');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .markdown id="Rxzcpe7IE4em"}
### Додавање на сликите во grade.csv {#додавање-на-сликите-во-gradecsv}
:::

::: {.cell .code colab="{\"height\":532,\"base_uri\":\"https://localhost:8080/\"}" id="3XjYshg-8tSA" outputId="3f160a04-246b-47bf-bbb5-b99e91898173"}
``` {.python}
names_ordered = list(train_data["name"])
images_ordered = []
for name in names_ordered:
  images_ordered.append(Image.open('drive/MyDrive/images/' + name + '.bmp'))

train_data['image'] = images_ordered
train_data
```

::: {.output .stream .stderr}
    /usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      
:::

::: {.output .execute_result execution_count="31"}
```{=html}
  <div id="df-329970c4-ea5b-4e2d-ba45-da2af4fd6e6c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>patient ID</th>
      <th>grade (GlaS)</th>
      <th>grade (Sirinukunwattana et al. 2015)</th>
      <th>image</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>80</th>
      <td>train_1</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>81</th>
      <td>train_10</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>82</th>
      <td>train_11</td>
      <td>10</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>83</th>
      <td>train_12</td>
      <td>13</td>
      <td>benign</td>
      <td>healthy</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>84</th>
      <td>train_13</td>
      <td>1</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>160</th>
      <td>train_82</td>
      <td>2</td>
      <td>malignant</td>
      <td>moderately-to-poorly differentated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>161</th>
      <td>train_83</td>
      <td>11</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>162</th>
      <td>train_84</td>
      <td>15</td>
      <td>benign</td>
      <td>healthy</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>163</th>
      <td>train_85</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>164</th>
      <td>train_9</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-329970c4-ea5b-4e2d-ba45-da2af4fd6e6c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-329970c4-ea5b-4e2d-ba45-da2af4fd6e6c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-329970c4-ea5b-4e2d-ba45-da2af4fd6e6c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .code colab="{\"height\":532,\"base_uri\":\"https://localhost:8080/\"}" id="mZiuyIZT-Gar" outputId="02703451-9d81-42dd-ddc0-6281b54f1d28"}
``` {.python}
names_ordered = list(test_data["name"])
images_ordered = []
for name in names_ordered:
  images_ordered.append(Image.open('drive/MyDrive/images/' + name + '.bmp'))

test_data['image'] = images_ordered
test_data
```

::: {.output .stream .stderr}
    /usr/local/lib/python3.7/dist-packages/ipykernel_launcher.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      
:::

::: {.output .execute_result execution_count="32"}
```{=html}
  <div id="df-fc310226-e4d7-426d-8b16-a3334ba5b624">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>patient ID</th>
      <th>grade (GlaS)</th>
      <th>grade (Sirinukunwattana et al. 2015)</th>
      <th>image</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>testA_1</td>
      <td>4</td>
      <td>benign</td>
      <td>adenomatous</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>testA_10</td>
      <td>10</td>
      <td>benign</td>
      <td>healthy</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>testA_11</td>
      <td>9</td>
      <td>benign</td>
      <td>healthy</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>testA_12</td>
      <td>11</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>testA_13</td>
      <td>7</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>75</th>
      <td>testB_5</td>
      <td>5</td>
      <td>benign</td>
      <td>adenomatous</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>76</th>
      <td>testB_6</td>
      <td>3</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>77</th>
      <td>testB_7</td>
      <td>5</td>
      <td>benign</td>
      <td>adenomatous</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>78</th>
      <td>testB_8</td>
      <td>7</td>
      <td>malignant</td>
      <td>moderately differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
    <tr>
      <th>79</th>
      <td>testB_9</td>
      <td>1</td>
      <td>malignant</td>
      <td>poorly differentiated</td>
      <td>&lt;PIL.BmpImagePlugin.BmpImageFile image mode=RG...</td>
    </tr>
  </tbody>
</table>
<p>80 rows × 5 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-fc310226-e4d7-426d-8b16-a3334ba5b624')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">
        
  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>
      
  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-fc310226-e4d7-426d-8b16-a3334ba5b624 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-fc310226-e4d7-426d-8b16-a3334ba5b624');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>
  
```
:::
:::

::: {.cell .markdown id="L_bPMBiDYwjG"}
## Фаза 3 - Креирање на модели/Употреба на методи
:::

::: {.cell .markdown id="gi709ZNhigjj"}
Иснталација на постара верзија од keras и tensorflow за полесна
конфигурација на моделот
:::

::: {.cell .code colab="{\"height\":1000,\"base_uri\":\"https://localhost:8080/\"}" id="Uj4m_6zXRh2w" outputId="6ae873ec-ce45-4fd5-9e58-b049a8dc312b"}
``` {.python}
!pip install q keras==1.2.2
!pip install tensorflow==1.14.0
```

::: {.output .stream .stdout}
    Collecting q
      Downloading q-2.6-py2.py3-none-any.whl (6.8 kB)
    Collecting keras==1.2.2
      Downloading Keras-1.2.2.tar.gz (175 kB)
    ent already satisfied: pyyaml in /usr/local/lib/python3.7/dist-packages (from keras==1.2.2) (3.13)
    Requirement already satisfied: six in /usr/local/lib/python3.7/dist-packages (from keras==1.2.2) (1.15.0)
    Requirement already satisfied: numpy>=1.9.1 in /usr/local/lib/python3.7/dist-packages (from theano->keras==1.2.2) (1.19.5)
    Requirement already satisfied: scipy>=0.14 in /usr/local/lib/python3.7/dist-packages (from theano->keras==1.2.2) (1.4.1)
    Building wheels for collected packages: keras, theano
      Building wheel for keras (setup.py) ... e=Keras-1.2.2-py3-none-any.whl size=209601 sha256=7990587d9affdb2125d1b7300d75975ce017a771f8e0ea0ffee3560d511ae71f
      Stored in directory: /root/.cache/pip/wheels/d1/32/23/2a1db3765ec19c91503843380a4f92b6530598949c661c5fa2
      Building wheel for theano (setup.py) ... e=Theano-1.0.5-py3-none-any.whl size=2668111 sha256=4d81825a6d07a252012435462c795c7a7957c699a1ae0d1de6a89914c709e53b
      Stored in directory: /root/.cache/pip/wheels/26/68/6f/745330367ce7822fe0cd863712858151f5723a0a5e322cc144
    Successfully built keras theano
    Installing collected packages: theano, q, keras
      Attempting uninstall: keras
        Found existing installation: keras 2.7.0
        Uninstalling keras-2.7.0:
          Successfully uninstalled keras-2.7.0
    ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
    tensorflow 2.7.0 requires keras<2.8,>=2.7.0rc0, but you have keras 1.2.2 which is incompatible.
    Successfully installed keras-1.2.2 q-2.6 theano-1.0.5
:::

::: {.output .display_data}
``` {.json}
{"pip_warning":{"packages":["keras"]}}
```
:::

::: {.output .stream .stdout}
    Collecting tensorflow==1.14.0
      Downloading tensorflow-1.14.0-cp37-cp37m-manylinux1_x86_64.whl (109.3 MB)
    ator<1.15.0rc0,>=1.14.0rc0
      Downloading tensorflow_estimator-1.14.0-py2.py3-none-any.whl (488 kB)
    ent already satisfied: termcolor>=1.1.0 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (1.1.0)
    Requirement already satisfied: astor>=0.6.0 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (0.8.1)
    Collecting keras-applications>=1.0.6
      Downloading Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
    ent already satisfied: wrapt>=1.11.1 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (1.13.3)
    Requirement already satisfied: grpcio>=1.8.6 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (1.43.0)
    Collecting tensorboard<1.15.0,>=1.14.0
      Downloading tensorboard-1.14.0-py3-none-any.whl (3.1 MB)
    ent already satisfied: six>=1.10.0 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (1.15.0)
    Requirement already satisfied: gast>=0.2.0 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (0.4.0)
    Requirement already satisfied: numpy<2.0,>=1.14.5 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (1.19.5)
    Requirement already satisfied: absl-py>=0.7.0 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (0.12.0)
    Requirement already satisfied: wheel>=0.26 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (0.37.1)
    Requirement already satisfied: protobuf>=3.6.1 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (3.17.3)
    Requirement already satisfied: google-pasta>=0.1.6 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (0.2.0)
    Requirement already satisfied: keras-preprocessing>=1.0.5 in /usr/local/lib/python3.7/dist-packages (from tensorflow==1.14.0) (1.1.2)
    Requirement already satisfied: h5py in /usr/local/lib/python3.7/dist-packages (from keras-applications>=1.0.6->tensorflow==1.14.0) (3.1.0)
    Requirement already satisfied: werkzeug>=0.11.15 in /usr/local/lib/python3.7/dist-packages (from tensorboard<1.15.0,>=1.14.0->tensorflow==1.14.0) (1.0.1)
    Requirement already satisfied: setuptools>=41.0.0 in /usr/local/lib/python3.7/dist-packages (from tensorboard<1.15.0,>=1.14.0->tensorflow==1.14.0) (57.4.0)
    Requirement already satisfied: markdown>=2.6.8 in /usr/local/lib/python3.7/dist-packages (from tensorboard<1.15.0,>=1.14.0->tensorflow==1.14.0) (3.3.6)
    Requirement already satisfied: importlib-metadata>=4.4 in /usr/local/lib/python3.7/dist-packages (from markdown>=2.6.8->tensorboard<1.15.0,>=1.14.0->tensorflow==1.14.0) (4.10.0)
    Requirement already satisfied: typing-extensions>=3.6.4 in /usr/local/lib/python3.7/dist-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<1.15.0,>=1.14.0->tensorflow==1.14.0) (3.10.0.2)
    Requirement already satisfied: zipp>=0.5 in /usr/local/lib/python3.7/dist-packages (from importlib-metadata>=4.4->markdown>=2.6.8->tensorboard<1.15.0,>=1.14.0->tensorflow==1.14.0) (3.7.0)
    Requirement already satisfied: cached-property in /usr/local/lib/python3.7/dist-packages (from h5py->keras-applications>=1.0.6->tensorflow==1.14.0) (1.5.2)
    Installing collected packages: tensorflow-estimator, tensorboard, keras-applications, tensorflow
      Attempting uninstall: tensorflow-estimator
        Found existing installation: tensorflow-estimator 2.7.0
        Uninstalling tensorflow-estimator-2.7.0:
          Successfully uninstalled tensorflow-estimator-2.7.0
      Attempting uninstall: tensorboard
        Found existing installation: tensorboard 2.7.0
        Uninstalling tensorboard-2.7.0:
          Successfully uninstalled tensorboard-2.7.0
      Attempting uninstall: tensorflow
        Found existing installation: tensorflow 2.7.0
        Uninstalling tensorflow-2.7.0:
          Successfully uninstalled tensorflow-2.7.0
    ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
    kapre 0.3.6 requires tensorflow>=2.0.0, but you have tensorflow 1.14.0 which is incompatible.
    Successfully installed keras-applications-1.0.8 tensorboard-1.14.0 tensorflow-1.14.0 tensorflow-estimator-1.14.0
:::

::: {.output .display_data}
``` {.json}
{"pip_warning":{"packages":["tensorboard","tensorflow"]}}
```
:::
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="skQCz5T4RnKW" outputId="cb06ea4a-d25f-4444-ea38-4820d7e56384"}
``` {.python}
import keras
import tensorflow as tf
print(keras.__version__)
print(tf.__version__)
```

::: {.output .stream .stderr}
    Using TensorFlow backend.
    /usr/local/lib/python3.7/dist-packages/tensorflow/python/framework/dtypes.py:516: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_qint8 = np.dtype([("qint8", np.int8, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorflow/python/framework/dtypes.py:517: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorflow/python/framework/dtypes.py:518: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_qint16 = np.dtype([("qint16", np.int16, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorflow/python/framework/dtypes.py:519: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorflow/python/framework/dtypes.py:520: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_qint32 = np.dtype([("qint32", np.int32, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorflow/python/framework/dtypes.py:525: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      np_resource = np.dtype([("resource", np.ubyte, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:541: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_qint8 = np.dtype([("qint8", np.int8, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:542: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_quint8 = np.dtype([("quint8", np.uint8, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:543: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_qint16 = np.dtype([("qint16", np.int16, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:544: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_quint16 = np.dtype([("quint16", np.uint16, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:545: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      _np_qint32 = np.dtype([("qint32", np.int32, 1)])
    /usr/local/lib/python3.7/dist-packages/tensorboard/compat/tensorflow_stub/dtypes.py:550: FutureWarning: Passing (type, 1) or '1type' as a synonym of type is deprecated; in a future version of numpy, it will be understood as (type, (1,)) / '(1,)type'.
      np_resource = np.dtype([("resource", np.ubyte, 1)])
:::

::: {.output .stream .stdout}
    1.2.2
    1.14.0
:::
:::

::: {.cell .markdown id="20GnNNKSqQKW"}
#### Делење на train и test множество
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="bRlf1nfarHiO" outputId="57368f95-3b6b-44c2-989c-c63cfe559df7"}
``` {.python}
import os 
import glob

file_paths = glob.glob("drive/MyDrive/images/*")
train_paths = [file_path for file_path in file_paths if "train" in file_path]
test_paths = [file_path for file_path in file_paths if "test" in file_path]
print("Number of train images: " + str(len(train_paths)))
print("Number of test images: " + str(len(test_paths)))
```

::: {.output .stream .stdout}
    Number of train images: 170
    Number of test images: 160
:::
:::

::: {.cell .markdown id="vF32blfxvkMp"}
#### Генерирање бинарна верзија од сликите
:::

::: {.cell .markdown id="knjkNdlZiukO"}
Дополнително предпроцесирање на податоците и генерирање на train и test
подмножеството.
:::

::: {.cell .code id="X5NNaQzHY4r4"}
``` {.python}
import os
import numpy as np

import cv2

image_rows = 522 # image height
image_cols = 775 # image width


def create_train_data():
    total = 85 # Train множеството без резултатите (без _anno)

    imgs = np.ndarray((total, 1, image_rows, image_cols), dtype=np.uint8)
    imgs_mask = np.ndarray((total, 1, image_rows, image_cols), dtype=np.uint8)

    print('Creating training images...')
    i = 0
    for image_name in train_paths:
        if 'anno' in image_name:
            continue
        image_mask_name = image_name.split('.')[0] + '_anno.bmp'
        #Додавање _anno на бинарните верзии од сликите

        img = cv2.imread(image_name, cv2.IMREAD_GRAYSCALE)
        img = cv2.resize(img, (image_cols, image_rows))

        img_mask = cv2.imread(image_mask_name, cv2.IMREAD_GRAYSCALE)

        img_mask = cv2.resize(img_mask, (image_cols, image_rows))

        img = np.array([img])
        img_mask = np.array([img_mask])

        imgs[i] = img
        img_mask[img_mask != 0] = 255.0
        imgs_mask[i] = img_mask

        if i % 100 == 0:
            print('Done: {0}/{1} images'.format(i, total))
        i += 1

    print('Loading done.')

    np.save('imgs_train.npy', imgs)
    np.save('imgs_mask_train.npy', imgs_mask)
    print('Saving to .npy files done.')


def load_train_data():
    imgs_train = np.load('imgs_train.npy')
    imgs_mask_train = np.load('imgs_mask_train.npy')
    return imgs_train, imgs_mask_train


def create_test_data():
    total = 80

    imgs = np.ndarray((total, 1, image_rows, image_cols), dtype=np.uint8)

    i = 0
    print('-'*30)
    print('Creating test images...')
    print('-'*30)
    for image_name in test_paths:
        if 'anno' in image_name:
            continue
        img = cv2.imread(image_name, cv2.IMREAD_GRAYSCALE)
        img = cv2.resize(img, (image_cols, image_rows))
        
        img = np.array([img])

        imgs[i] = img

    print('Loading done.')

    np.save('imgs_test.npy', imgs)
    print('Saving to .npy files done.')


def load_test_data():
    imgs_test = np.load('imgs_test.npy')
    return imgs_test
```
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="2Qe7QpwBwR47" outputId="4d12102e-f266-49a4-b864-b1e59a2ca78d"}
``` {.python}
create_train_data()
create_test_data()
```

::: {.output .stream .stdout}
    Creating training images...
    Done: 0/85 images
    Loading done.
    Saving to .npy files done.
    ------------------------------
    Creating test images...
    ------------------------------
    Loading done.
    Saving to .npy files done.
:::
:::

::: {.cell .markdown id="5J7mNwAhvuRg"}
#### Читање и тренирање на моделот
:::

::: {.cell .markdown id="GdZpv_zIkES4"}
Главно се користи keras пајтон библиотеката

-   Сликите ги намалуваме на висина 100 пиксели и ширина 160 пиксели со
    помош на preprocess функцијата користејќи INTER_CUBIC техника на
    намалување на резолуција од cv2 библиотеката

-   Моделот е со пет слоја каде во секоја слој има:

-   -   Convolutional2D

-   -   LeakyRelu activation function

-   -   SpatialDropout2D ја има истата функција како Dropout, но во
        SpatialDropout2D отфрлува цели 2D feature maps (со ова се
        подобруваат независностите на feature maps-от)

-   -   AveragePooling2D ја намалува димензијата на сликата, односно
        (2, 2) значи намалување на ширината и висината на сликата за
        пола
:::

::: {.cell .code id="U5S0amIxNzZo"}
``` {.python}
import cv2
import numpy as np
from keras.models import Model
from keras.layers.advanced_activations import LeakyReLU
from keras.layers import Input, merge, SpatialDropout2D
from keras.layers import Convolution2D, AveragePooling2D, UpSampling2D
from keras.optimizers import Adam
from keras.callbacks import ModelCheckpoint, EarlyStopping
from keras.preprocessing.image import ImageDataGenerator
from keras import backend as K


K.set_image_dim_ordering('th')  # Theano dimension ordering in this code

img_rows = 100
img_cols = 160
stack = 10

smooth = 1.


def dice_coef(y_true, y_pred):
    y_true_f = K.flatten(y_true)
    y_pred_f = K.flatten(y_pred)
    intersection = K.sum(y_true_f * y_pred_f)
    return (2. * intersection + smooth) / (K.sum(y_true_f) + K.sum(y_pred_f) + smooth)


def dice_coef_loss(y_true, y_pred):
    return -dice_coef(y_true, y_pred)


def create_model():
    input = Input(shape=(1, img_rows, img_cols))
    
    conv1 = Convolution2D(32, 3, 3, border_mode='same', init='he_normal')(input)
    conv1 = LeakyReLU()(conv1)
    conv1 = SpatialDropout2D(0.2)(conv1)
    conv1 = Convolution2D(32, 3, 3, border_mode='same', init='he_normal')(conv1)
    conv1 = LeakyReLU()(conv1)
    conv1 = SpatialDropout2D(0.2)(conv1)
    pool1 = AveragePooling2D(pool_size=(2,2))(conv1)
    
    conv2 = Convolution2D(64, 3, 3, border_mode='same', init='he_normal')(pool1)
    conv2 = LeakyReLU()(conv2)
    conv2 = SpatialDropout2D(0.2)(conv2)
    conv2 = Convolution2D(64, 3, 3, border_mode='same', init='he_normal')(conv2)
    conv2 = LeakyReLU()(conv2)
    conv2 = SpatialDropout2D(0.2)(conv2)
    pool2 = AveragePooling2D(pool_size=(2,2))(conv2)
    
    conv3 = Convolution2D(128, 3, 3, border_mode='same', init='he_normal')(pool2)
    conv3 = LeakyReLU()(conv3)
    conv3 = SpatialDropout2D(0.2)(conv3)
    conv3 = Convolution2D(128, 3, 3, border_mode='same', init='he_normal')(conv3)
    conv3 = LeakyReLU()(conv3)
    conv3 = SpatialDropout2D(0.2)(conv3)
    
    comb1 = merge([conv2, UpSampling2D(size=(2,2))(conv3)], mode='concat', concat_axis=1)
    conv4 = Convolution2D(64, 3, 3, border_mode='same', init='he_normal')(comb1)
    conv4 = LeakyReLU()(conv4)
    conv4 = SpatialDropout2D(0.2)(conv4)
    conv4 = Convolution2D(64, 3, 3, border_mode='same', init='he_normal')(conv4)
    conv4 = LeakyReLU()(conv4)
    conv4 = SpatialDropout2D(0.2)(conv4)
    
    comb2 = merge([conv1, UpSampling2D(size=(2,2))(conv4)], mode='concat', concat_axis=1)
    conv5 = Convolution2D(32, 3, 3, border_mode='same', init='he_normal')(comb2)
    conv5 = LeakyReLU()(conv5)
    conv5 = SpatialDropout2D(0.2)(conv5)
    conv5 = Convolution2D(32, 3, 3, border_mode='same', init='he_normal')(conv5)
    conv5 = LeakyReLU()(conv5)
    conv5 = SpatialDropout2D(0.2)(conv5)
    
    output = Convolution2D(1, 1, 1, activation='sigmoid')(conv5)

    model = Model(input=input, output=output)
    model.compile(optimizer=Adam(lr=3e-4), loss='binary_crossentropy')
    return model


def preprocess(imgs):
    imgs_p = np.ndarray((imgs.shape[0], imgs.shape[1], img_rows, img_cols), dtype=np.uint8)
    for i in range(imgs.shape[0]):
        imgs_p[i, 0] = cv2.resize(imgs[i, 0], (img_cols, img_rows), interpolation=cv2.INTER_CUBIC)
    return imgs_p
```
:::

::: {.cell .markdown id="lp1isdP_ocLb"}
Сумаризација на моделот:
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="ncFFupTXfHcq" outputId="6665f40e-560e-44ba-bd82-7b0a9c70f0c5"}
``` {.python}
model.summary()
```

::: {.output .stream .stdout}
    ____________________________________________________________________________________________________
    Layer (type)                     Output Shape          Param #     Connected to                     
    ====================================================================================================
    input_1 (InputLayer)             (None, 1, 100, 160)   0                                            
    ____________________________________________________________________________________________________
    convolution2d_1 (Convolution2D)  (None, 32, 100, 160)  320         input_1[0][0]                    
    ____________________________________________________________________________________________________
    leakyrelu_1 (LeakyReLU)          (None, 32, 100, 160)  0           convolution2d_1[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_1 (SpatialDropo (None, 32, 100, 160)  0           leakyrelu_1[0][0]                
    ____________________________________________________________________________________________________
    convolution2d_2 (Convolution2D)  (None, 32, 100, 160)  9248        spatialdropout2d_1[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_2 (LeakyReLU)          (None, 32, 100, 160)  0           convolution2d_2[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_2 (SpatialDropo (None, 32, 100, 160)  0           leakyrelu_2[0][0]                
    ____________________________________________________________________________________________________
    averagepooling2d_1 (AveragePooli (None, 32, 50, 80)    0           spatialdropout2d_2[0][0]         
    ____________________________________________________________________________________________________
    convolution2d_3 (Convolution2D)  (None, 64, 50, 80)    18496       averagepooling2d_1[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_3 (LeakyReLU)          (None, 64, 50, 80)    0           convolution2d_3[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_3 (SpatialDropo (None, 64, 50, 80)    0           leakyrelu_3[0][0]                
    ____________________________________________________________________________________________________
    convolution2d_4 (Convolution2D)  (None, 64, 50, 80)    36928       spatialdropout2d_3[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_4 (LeakyReLU)          (None, 64, 50, 80)    0           convolution2d_4[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_4 (SpatialDropo (None, 64, 50, 80)    0           leakyrelu_4[0][0]                
    ____________________________________________________________________________________________________
    averagepooling2d_2 (AveragePooli (None, 64, 25, 40)    0           spatialdropout2d_4[0][0]         
    ____________________________________________________________________________________________________
    convolution2d_5 (Convolution2D)  (None, 128, 25, 40)   73856       averagepooling2d_2[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_5 (LeakyReLU)          (None, 128, 25, 40)   0           convolution2d_5[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_5 (SpatialDropo (None, 128, 25, 40)   0           leakyrelu_5[0][0]                
    ____________________________________________________________________________________________________
    convolution2d_6 (Convolution2D)  (None, 128, 25, 40)   147584      spatialdropout2d_5[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_6 (LeakyReLU)          (None, 128, 25, 40)   0           convolution2d_6[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_6 (SpatialDropo (None, 128, 25, 40)   0           leakyrelu_6[0][0]                
    ____________________________________________________________________________________________________
    upsampling2d_1 (UpSampling2D)    (None, 128, 50, 80)   0           spatialdropout2d_6[0][0]         
    ____________________________________________________________________________________________________
    merge_1 (Merge)                  (None, 192, 50, 80)   0           spatialdropout2d_4[0][0]         
                                                                       upsampling2d_1[0][0]             
    ____________________________________________________________________________________________________
    convolution2d_7 (Convolution2D)  (None, 64, 50, 80)    110656      merge_1[0][0]                    
    ____________________________________________________________________________________________________
    leakyrelu_7 (LeakyReLU)          (None, 64, 50, 80)    0           convolution2d_7[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_7 (SpatialDropo (None, 64, 50, 80)    0           leakyrelu_7[0][0]                
    ____________________________________________________________________________________________________
    convolution2d_8 (Convolution2D)  (None, 64, 50, 80)    36928       spatialdropout2d_7[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_8 (LeakyReLU)          (None, 64, 50, 80)    0           convolution2d_8[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_8 (SpatialDropo (None, 64, 50, 80)    0           leakyrelu_8[0][0]                
    ____________________________________________________________________________________________________
    upsampling2d_2 (UpSampling2D)    (None, 64, 100, 160)  0           spatialdropout2d_8[0][0]         
    ____________________________________________________________________________________________________
    merge_2 (Merge)                  (None, 96, 100, 160)  0           spatialdropout2d_2[0][0]         
                                                                       upsampling2d_2[0][0]             
    ____________________________________________________________________________________________________
    convolution2d_9 (Convolution2D)  (None, 32, 100, 160)  27680       merge_2[0][0]                    
    ____________________________________________________________________________________________________
    leakyrelu_9 (LeakyReLU)          (None, 32, 100, 160)  0           convolution2d_9[0][0]            
    ____________________________________________________________________________________________________
    spatialdropout2d_9 (SpatialDropo (None, 32, 100, 160)  0           leakyrelu_9[0][0]                
    ____________________________________________________________________________________________________
    convolution2d_10 (Convolution2D) (None, 32, 100, 160)  9248        spatialdropout2d_9[0][0]         
    ____________________________________________________________________________________________________
    leakyrelu_10 (LeakyReLU)         (None, 32, 100, 160)  0           convolution2d_10[0][0]           
    ____________________________________________________________________________________________________
    spatialdropout2d_10 (SpatialDrop (None, 32, 100, 160)  0           leakyrelu_10[0][0]               
    ____________________________________________________________________________________________________
    convolution2d_11 (Convolution2D) (None, 1, 100, 160)   33          spatialdropout2d_10[0][0]        
    ====================================================================================================
    Total params: 470,977
    Trainable params: 470,977
    Non-trainable params: 0
    ____________________________________________________________________________________________________
:::
:::

::: {.cell .markdown id="mgkOn9G6pETt"}
Со тестирање на повеќе различни конволуциски мрежи одлучив со горниот
модел да продолжам, бидејќи добив најдобри резултати со извршување на
моделот со една епоха (10 минути). Но за крајниот модел ќе треба над 50
епохи да се извршат што ќе трае долго.
:::

::: {.cell .markdown id="BVsMgNXVYNI-"}
\#\#Фаза 4
:::

::: {.cell .markdown id="WEaA6dRZTVlV"}
#### Процесирање на податоците (скалирање на пикселите за побрза конвергенција на моделот)
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="EXdQf363TbGT" outputId="d8d6e410-d82c-4eb6-ef7b-70e5c8a55eb4"}
``` {.python}
print('-'*30)
print('Loading and preprocessing train data...')
print('-'*30)
imgs_train, imgs_mask_train = load_train_data()

imgs_train = preprocess(imgs_train)
imgs_mask_train = preprocess(imgs_mask_train)

imgs_train = imgs_train.astype('float32')
mean = np.mean(imgs_train)  
std = np.std(imgs_train)

imgs_train -= mean
imgs_train /= std

imgs_mask_train = imgs_mask_train.astype('float32')
imgs_mask_train /= 255.  # scale masks to [0, 1]
```

::: {.output .stream .stdout}
    ------------------------------
    Loading and preprocessing train data...
    ------------------------------
:::
:::

::: {.cell .markdown id="P44-ElwTTgrU"}
#### Компајлирање
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="yvJdsXLuTj1z" outputId="f6e27b90-cb47-46ce-e692-8543e517a563"}
``` {.python}
print('-'*30)
print('Creating and compiling model...')
print('-'*30)
model = create_model()

print('-'*30)
print('Building data augmentation object...')
print('-'*30)
datagen = ImageDataGenerator(
    rotation_range=15,
    width_shift_range=0.15,
    height_shift_range=0.15,
    shear_range=0.15,
    horizontal_flip=True,
    vertical_flip=True)
    
total = imgs_train.shape[0]
img = []
count = 0
for batch in datagen.flow(imgs_train, batch_size=1, seed=1337):
    img.append(batch)
    count += 1
    if count > total*stack:
        break
imgs_train = np.array(img)[:,0]

mask = [] 
count = 0
for batch in datagen.flow(imgs_mask_train, batch_size=1, seed=1337): 
    mask.append(batch)
    count += 1
    if count > total*stack:
        break
imgs_mask_train = np.array(mask)[:,0]
    
callbacks = [
    EarlyStopping(monitor='loss', patience=5, verbose=0),
    ModelCheckpoint('drive/MyDrive/weights1.hdf5', monitor='loss', save_best_only=True)
]
```

::: {.output .stream .stdout}
    ------------------------------
    Creating and compiling model...
    ------------------------------
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:321: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:673: calling RandomNormal.__init__ (from tensorflow.python.ops.init_ops) with dtype is deprecated and will be removed in a future version.
    Instructions for updating:
    Call initializer instance with the dtype argument instead of passing it to the constructor
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:491: calling Constant.__init__ (from tensorflow.python.ops.init_ops) with dtype is deprecated and will be removed in a future version.
    Instructions for updating:
    Call initializer instance with the dtype argument instead of passing it to the constructor
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:73: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:2516: calling dropout (from tensorflow.python.ops.nn_ops) with keep_prob is deprecated and will be removed in a future version.
    Instructions for updating:
    Please use `rate` instead of `keep_prob`. Rate should be set to `rate = 1 - keep_prob`.
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:2868: The name tf.nn.avg_pool is deprecated. Please use tf.nn.avg_pool2d instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:1497: The name tf.image.resize_nearest_neighbor is deprecated. Please use tf.compat.v1.image.resize_nearest_neighbor instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:634: calling RandomUniform.__init__ (from tensorflow.python.ops.init_ops) with dtype is deprecated and will be removed in a future version.
    Instructions for updating:
    Call initializer instance with the dtype argument instead of passing it to the constructor
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/optimizers.py:658: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:2446: The name tf.log is deprecated. Please use tf.math.log instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/tensorflow/python/ops/nn_impl.py:180: add_dispatch_support.<locals>.wrapper (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
    Instructions for updating:
    Use tf.where in 2.0, which has the same broadcast rule as np.where
    ------------------------------
    Building data augmentation object...
    ------------------------------
:::
:::

::: {.cell .markdown id="vPPJ3SyNTmoS"}
#### Тренирање на моделот со 25 епохи (време на тренирање одприлика 2 саати)
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="M624b4CMUD1U" outputId="bc9e04a0-bd0c-4f8f-f642-e43c1e0f63fe"}
``` {.python}
print('-'*30)
print('Begin training...')
print('-'*30)
model.fit(imgs_train, imgs_mask_train, batch_size=4, nb_epoch=25, verbose=1, shuffle=True,callbacks=callbacks)
```

::: {.output .stream .stdout}
    ------------------------------
    Begin training...
    ------------------------------
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:740: The name tf.assign_add is deprecated. Please use tf.compat.v1.assign_add instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:736: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

    Epoch 1/25
    851/851 [==============================] - 311s - loss: 0.7209   
    Epoch 2/25
    851/851 [==============================] - 298s - loss: 0.6682   
    Epoch 3/25
    851/851 [==============================] - 299s - loss: 0.6509   
    Epoch 4/25
    851/851 [==============================] - 297s - loss: 0.6313   
    Epoch 5/25
    851/851 [==============================] - 301s - loss: 0.6174   
    Epoch 6/25
    851/851 [==============================] - 303s - loss: 0.5982   
    Epoch 7/25
    851/851 [==============================] - 301s - loss: 0.5903   
    Epoch 8/25
    851/851 [==============================] - 301s - loss: 0.5822   
    Epoch 9/25
    851/851 [==============================] - 300s - loss: 0.5794   
    Epoch 10/25
    851/851 [==============================] - 299s - loss: 0.5710   
    Epoch 11/25
    851/851 [==============================] - 298s - loss: 0.5620   
    Epoch 12/25
    851/851 [==============================] - 302s - loss: 0.5529   
    Epoch 13/25
    851/851 [==============================] - 303s - loss: 0.5499   
    Epoch 14/25
    851/851 [==============================] - 299s - loss: 0.5483   
    Epoch 15/25
    851/851 [==============================] - 302s - loss: 0.5368   
    Epoch 16/25
    851/851 [==============================] - 302s - loss: 0.5331   
    Epoch 17/25
    851/851 [==============================] - 300s - loss: 0.5284   
    Epoch 18/25
    851/851 [==============================] - 303s - loss: 0.5254   
    Epoch 19/25
    851/851 [==============================] - 301s - loss: 0.5181   
    Epoch 20/25
    851/851 [==============================] - 302s - loss: 0.5145   
    Epoch 21/25
    851/851 [==============================] - 301s - loss: 0.5111   
    Epoch 22/25
    851/851 [==============================] - 297s - loss: 0.5070   
    Epoch 23/25
    851/851 [==============================] - 298s - loss: 0.4983   
    Epoch 24/25
    851/851 [==============================] - 297s - loss: 0.4998   
    Epoch 25/25
    851/851 [==============================] - 299s - loss: 0.4937   
    ------------------------------
    Loading and preprocessing test data...
    ------------------------------
:::
:::

::: {.cell .markdown id="kPupmWRww6wP"}
#### Предпроцесирање на test множеството
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="sl__d8Tee2I0" outputId="100311d2-dab6-47b3-c8e2-67b98ed40af1"}
``` {.python}
print('-'*30)
print('Loading and preprocessing test data...')
print('-'*30)
imgs_test = load_test_data()
imgs_test = preprocess(imgs_test)

imgs_test = imgs_test.astype('float32')
imgs_test -= mean
imgs_test /= std
```

::: {.output .stream .stdout}
    ------------------------------
    Loading and preprocessing test data...
    ------------------------------
:::
:::

::: {.cell .markdown id="GRmQIs_gUKlq"}
#### Во случај да треба од поново да го тестирам моделот, ги зачував тежините на моделот
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="f_BVK_87UM7T" outputId="7b9c4671-110e-4fc4-8b37-4a104493a03c"}
``` {.python}
print('-'*30)
print('Loading saved weights...')
print('-'*30)
model.load_weights('drive/MyDrive/weights.hdf5')
```

::: {.output .stream .stdout}
    ------------------------------
    Loading saved weights...
    ------------------------------
    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:112: The name tf.get_default_session is deprecated. Please use tf.compat.v1.get_default_session instead.

    WARNING:tensorflow:From /usr/local/lib/python3.7/dist-packages/keras/backend/tensorflow_backend.py:117: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.
:::
:::

::: {.cell .markdown id="0nQ7_ALSUQLK"}
#### Тестирање, и зачувување на резултатите
:::

::: {.cell .code colab="{\"base_uri\":\"https://localhost:8080/\"}" id="J43l_MLiURaw" outputId="82069c62-4ade-4ee3-d284-1ad50ceea6e4"}
``` {.python}
print('-'*30)
print('Predicting masks on test data...')
print('-'*30)
imgs_mask_test = model.predict(imgs_test, verbose=1)
np.save('imgs_mask_test.npy', imgs_mask_test)
```

::: {.output .stream .stdout}
    ------------------------------
    Predicting masks on test data...
    ------------------------------
    80/80 [==============================] - 8s     
:::
:::

::: {.cell .markdown id="Io3D6uabifue"}
#### Визуелизација на резултатите
:::

::: {.cell .code id="WHDdhNIQhsHP"}
``` {.python}
import numpy as np
import cv2

image_rows = 522 # image height
image_cols = 775 # image width

def prep(img):
    img = img.astype('float32')
    img = cv2.threshold(img, 0.50, 1., cv2.THRESH_BINARY)[1].astype(np.uint8)
    img = cv2.resize(img, (image_cols, image_rows))
    return img


def run_length_enc(label):
    from itertools import chain
    x = label.transpose().flatten()
    y = np.where(x > 0)[0]
    if len(y) < 10:  # consider as empty
        return ''
    z = np.where(np.diff(y) > 1)[0]
    start = np.insert(y[z+1], 0, y[0])
    end = np.append(y[z], y[-1])
    length = end - start
    res = [[s+1, l+1] for s, l in zip(list(start), list(length))]
    res = list(chain.from_iterable(res))
    return ' '.join([str(r) for r in res])


def submission():
    imgs_test, imgs_id_test = load_test_data()
    imgs_test = np.load('imgs_mask_test.npy')

    argsort = np.argsort(imgs_id_test)
    imgs_id_test = imgs_id_test[argsort]
    imgs_test = imgs_test[argsort]

    total = imgs_test.shape[0]
    ids = []
    rles = []
    for i in range(total):
        img = imgs_test[i, 0]
        img = prep(img)
        rle = run_length_enc(img)

        rles.append(rle)
        ids.append(imgs_id_test[i])

        if i % 100 == 0:
            print('{}/{}'.format(i, total))

    first_row = 'img,pixels'
    file_name = 'submission.csv'

    with open(file_name, 'w+') as f:
        f.write(first_row + '\n')
        for i in range(total):
            s = str(ids[i]) + ',' + rles[i]
            f.write(s + '\n')
```
:::

::: {.cell .code id="sLhS2rGjdk1W"}
``` {.python}
import cv2
import numpy as np
import matplotlib.pyplot as plt



def visualize_results():
    images  = np.load('imgs_test.npy')
    results = np.load('imgs_mask_test.npy')
    
    total = results.shape[0]
    for i in range(total):
        f, axarr = plt.subplots(1,2)
        image = images[i,0]
        image = cv2.resize(image, (image_cols, image_rows))
        result = results[i,0]
        result = prep(result)

        axarr[0].imshow(image, cmap='Greys')
        axarr[1].imshow(result, alpha=0.30)
        plt.show()
```
:::

::: {.cell .code colab="{\"height\":1000,\"base_uri\":\"https://localhost:8080/\"}" id="8FoWx4adiGSW" outputId="55e5acc2-cb5d-45b9-955b-891c8c6e60a2"}
``` {.python}
visualize_results()
```

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/982534ad1c1546a54249a387f491e2d57019dd02.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1b482e89fc56e275ccf8bfc007fb13e5e27a1f32.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/99b8f059fa190e7f50e7e7e5751363d1c8cdb6d7.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/ba07be9e1f951f73223d564fd1dba39b735389e4.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1ee6962e51446bf52eec5a3d616af79988787887.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/d42b12026397e8a203ca6f0ae197af24eeb14940.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/192368af893cee1786ec824c12e9cab4682e9d83.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/bc05cfeab58429b6310f92600d3ad70e26d486b9.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/61c8cc0353adb57325aba3c58ab19a85951bc030.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/05b15f137f853c89759dc9c7930346045ea55a44.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/9e989a38e88128fac357cf27f6bd89e54eb8a8b7.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/11e0802f457f96996da4e56e58aaad0120e48b76.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/d6008dfd7bb1e94300cbffba945a8201dfac4dcd.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/ce615d056296211bf6ddd12fd7a409e61a2e5def.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/a84d24957ad94e462bd54adeb12152ab5c6c2a54.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/6c75ade4572d261eb0f06f9cdd4e1b75fef5ae45.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/a7c7f35f905d1df16d4e5c13588c94f92bd181b1.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/0b6ebd051a07e3350670e74149d63aca88d44b84.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/511407f02cdd41457609ff5021d88d99218da4f7.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/6db0aada770ecb5bf92752202e0b9f629a3d5dfa.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/8358613ae0989918195e0aed1893751ab37a20e8.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/bd28cdd53d4b3b82924ffd00d924f3084962b128.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/c6be7ffafa9a64d35a3cdb1df622fcf403c3c99a.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/169e419ac9ab9ae0859b5fbbdb72fe0283ee0f17.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1e81c951632487a93a3c924352f0ab65799ac643.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/cd77a0037e26d6a880f541e793db803fbb177b7d.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/a68b27397dd0a5af2a6e5d88946d2c466187d6ac.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/eebacd0bba75fe810715948588e623351a5b45ad.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/9b5634ea1e9020909f0d1b87e95c97c8d54fef0b.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/8820843ef87effbb030c1475b59af22ec038f841.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/2a337737bba6e26b47f19a55335fabcfc1d37975.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/c86aefe815ecb760046e2d4c058bc1ddba90b9d0.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/911b6b026a1c87c0cc746c16ff546e2a3d3d3507.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/a38a6c60de54f9ac1b53829347e5516dbbfa6cb9.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/5aef35abe1ddc613e417ec9729e9f61e3c4cd9b9.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1d9b87db7f1ff1331fbb9f2052634b231b162811.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1742011d2908a95ed2e1253f50fc9acefda1990f.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/fe5066966ef995734e28ba988438d977561143b4.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/f11e7349d6857c7df00a1d8fb8adfaca6fa782e3.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/9da15d6e16b26e668621d8b3da1d01fcbb58531c.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/4c07cf79f8aeed2efe59c3ee974b8f0260c1049c.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/18181624071e06aa9a89dbb92f26c73376124a91.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/c4a9a7c87d4b2e9f867ccdfa3dd3daee071f5bfc.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/187a4ee2d617b5b226689103a5e0f4b3d9c022c6.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/03a55cab6e517b200c0f64235dcec23bc9320a02.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/f8205249df640e2784f9493eade93ad2a6724a05.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/3164a7fc2c5976e862cd44ac195cd331261e3e7b.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/0935cc1ead4d30c2632ba25a8a995fa031de6500.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/153ec194995301c2fca820cb5f3dbf192194f333.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/e54a3ffad5f569b3d5e8246d5716c2e4254e7040.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/40a29b9d140f17592c4431b8cef18711cb533617.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/42e123a055b38c5bbab09917459b49373a4351a4.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/e99d6d0d367509c3c5d59a4298ee6b1f0735eca3.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/fca82133a2fc37b5ab562de142e2713dff82963c.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/9b2df56ce5f5fc8807b170823254798ba6bc8165.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/138a5e1b660a87137496f673ade939ded3e1915f.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/7ceb129af9e3f59924f334d71525d534958070f9.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/d15cdc345de8ec7856b37e65c65743a256a9cdd3.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/511fdc09a37f03a0ddb172633c819c68e464f3be.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/6698c70b6361bc95451f22b6033a3946afc62441.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/e747a9580fb7de5871af5210369646f4a97166a0.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/a933800978a2ac80722ac89c8661f2d729cdc432.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/3802a8a5d4b9fad9d2f39dcce74c4cf1a693d2f1.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/a80e685ec816b083af2cecc793500734b8d29988.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/825f53edd99a89f45ba7c551f6ebd598b2cb80a9.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/6f6839ec0995157e99695769a255bc66196230de.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/57effbc80c993539413eb63e72fc50c37777a6b1.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/23694b9c9592c7da046371162727dd4fb99188df.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/496e3cb220cef1bebdfd2378b341442ff39716ad.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/344b69cda2b834ab8d7e603fc62a303fad0cc0f3.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/ab5b0e63db4bee32b5f756204e04abc0645a552a.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/8f57076ba92adce0f13470adb77bac536afdbd0c.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1f8587d39d5f0cfb6c6da63215ba4b45147c588a.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/3b3b1e04fd1e94d296d785c4b9cfd6c8b4bd2587.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/754c50d9e40808bb058bda61a5f3764300ca87db.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/1e60d9b3e52988a7cfccae247831f7256a249001.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/c7408247e37c984e654544be17d9e621070b598d.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/d50cd4d588e78d26aff0c7deee11c0962aa841a1.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/e43f3d564033a844e58885e1cf57c955f1b24a2a.png)
:::

::: {.output .display_data}
![](vertopal_e33fbd16a2164a8d99b5c40a1517a548/27cd0b121f05d9881362d65949a1bdfbb13be832.png)
:::
:::
