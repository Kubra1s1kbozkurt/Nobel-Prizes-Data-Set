https://github.com/Kubra1s1kbozkurt/Nobel-Prizes-Data-Set/blob/main/PP.jpg
**Python Blok Projesi**<p><img style="float: right;margin:5px 20px 5px 1px; max-width:250px" src="https://assets.datacamp.com/production/project_441/img/Nobel_Prize.png"></p>

<p>Nobel Ödülü belki de dünyanın en tanınmış bilimsel ödülüdür. Her yıl kimya, edebiyat, fizik, tıp, ekonomi ve barış alanlarında bilim insanlarına ve akademisyenlere verilmektedir. Bu projede, Nobel Ödülü kazananları inceleyeceğiz. </p>

## Proje Soruları

1. Nobel Ödüllerini en çok kazanan ilk on ülkeyi bulunuz.
2. Nobel Ödüllerini kazanan ilk kadınları listeleyiniz.
3. Nobel Ödüllerini kazanan ilk erkekleri listeleyiniz.
4. Nobel ödülünü en çok kazanan ülkenin hangi yıldan itibaren hakimiyet sağladığını görselleştirip bu hakimiyette rol oynayan şeyler nelerdir? İçgörülerinizi paylaşır mısınız?
5. Nobel Ödülü kazananların cinsiyetlerini, yaşlarını, ödül kategorisi ve yılları kullanarak görselleştiriniz.(Her bir ödül kategorisi için ayrı grafik gösteriniz) Çıkan sonuçlara göre görseli yorumlayınız.
6. 1938-1945 yılı arasında Nobel Ödülü kazananların kategorilerini ve ülkelerini görselleştirip yorumlayınız.
7. 1947-1991 yılları arasında Nobel Ödülü kazananların kategorilerini ve ülkelerini görselleştirip yorumlayınız.(Her kategori için ayrı bir grafik olması istenmektedir)
8. Kimya, Edebiyat, Barış, Fizik ve Tıp kategorilerindeki 2000 sonrasındaki kişilerin ülkelerini, yaşlarını görselleştirin.(Her bir Kategori için ayrı görselleştirme yapılması istenmektedir) Veriyi yorumlayınız.



```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt 
import seaborn as sns
```


```python
df = pd.read_csv("/Users/isikk/Downloads/proje.csv")
df.head()
```




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
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1901</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1901</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/1</td>
      <td>160</td>
      <td>Individual</td>
      <td>Jacobus Henricus van 't Hoff</td>
      <td>1852-08-30</td>
      <td>Rotterdam</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Berlin University</td>
      <td>Berlin</td>
      <td>Germany</td>
      <td>1911-03-01</td>
      <td>Berlin</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1901</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1901</td>
      <td>"in special recognition of his poetic composit...</td>
      <td>1/1</td>
      <td>569</td>
      <td>Individual</td>
      <td>Sully Prudhomme</td>
      <td>1839-03-16</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1907-09-07</td>
      <td>Châtenay</td>
      <td>France</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1901</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1901</td>
      <td>"for his work on serum therapy, especially its...</td>
      <td>1/1</td>
      <td>293</td>
      <td>Individual</td>
      <td>Emil Adolf von Behring</td>
      <td>1854-03-15</td>
      <td>Hansdorf (Lawice)</td>
      <td>Prussia (Poland)</td>
      <td>Male</td>
      <td>Marburg University</td>
      <td>Marburg</td>
      <td>Germany</td>
      <td>1917-03-31</td>
      <td>Marburg</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1901</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>462</td>
      <td>Individual</td>
      <td>Jean Henry Dunant</td>
      <td>1828-05-08</td>
      <td>Geneva</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1910-10-30</td>
      <td>Heiden</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1901</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>463</td>
      <td>Individual</td>
      <td>Frédéric Passy</td>
      <td>1822-05-20</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1912-06-12</td>
      <td>Paris</td>
      <td>France</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape
```




    (911, 18)




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 911 entries, 0 to 910
    Data columns (total 18 columns):
     #   Column                Non-Null Count  Dtype 
    ---  ------                --------------  ----- 
     0   year                  911 non-null    int64 
     1   category              911 non-null    object
     2   prize                 911 non-null    object
     3   motivation            823 non-null    object
     4   prize_share           911 non-null    object
     5   laureate_id           911 non-null    int64 
     6   laureate_type         911 non-null    object
     7   full_name             911 non-null    object
     8   birth_date            883 non-null    object
     9   birth_city            883 non-null    object
     10  birth_country         885 non-null    object
     11  sex                   885 non-null    object
     12  organization_name     665 non-null    object
     13  organization_city     667 non-null    object
     14  organization_country  667 non-null    object
     15  death_date            593 non-null    object
     16  death_city            576 non-null    object
     17  death_country         582 non-null    object
    dtypes: int64(2), object(16)
    memory usage: 128.2+ KB
    


```python
df.isnull().sum()
```




    year                      0
    category                  0
    prize                     0
    motivation               88
    prize_share               0
    laureate_id               0
    laureate_type             0
    full_name                 0
    birth_date               28
    birth_city               28
    birth_country            26
    sex                      26
    organization_name       246
    organization_city       244
    organization_country    244
    death_date              318
    death_city              335
    death_country           329
    dtype: int64




```python
df.nunique()
```




    year                    113
    category                  6
    prize                   579
    motivation              565
    prize_share               4
    laureate_id             904
    laureate_type             2
    full_name               904
    birth_date              868
    birth_city              601
    birth_country           121
    sex                       2
    organization_name       295
    organization_city       181
    organization_country     29
    death_date              582
    death_city              291
    death_country            50
    dtype: int64



# 1-Nobel Ödüllerini en çok kazanan ilk on ülkeyi bulunuz.


```python
top_10_countries = df['birth_country'].value_counts().head(10)

print(top_10_countries)

```

    birth_country
    United States of America    259
    United Kingdom               85
    Germany                      61
    France                       51
    Sweden                       29
    Japan                        24
    Canada                       18
    Netherlands                  18
    Italy                        17
    Russia                       17
    Name: count, dtype: int64
    


```python
plt.figure(figsize=(10, 6))
top_10_countries.plot(kind='bar', color='gray')
plt.title('En Çok Nobel Ödülü Kazanan İlk 10 Ülke')
plt.xlabel('Ülke')
plt.ylabel('Kazanan Sayısı')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
```


    
![png](output_10_0.png)
    


# 2-Nobel Ödüllerini kazanan ilk kadınları listeleyiniz.


```python
df['sex'].unique()
```




    array(['Male', 'Female', nan], dtype=object)




```python
print(df["sex"].value_counts())

```

    sex
    Male      836
    Female     49
    Name: count, dtype: int64
    


```python
empty_sex = df['sex'].isnull().sum()
print("Boş 'sex' sütunu değer sayısı:", empty_sex)

```

    Boş 'sex' sütunu değer sayısı: 26
    


```python
#26 boş sütun içeriisinde isim üzerinden cinsiyet belirlemeye çalıştım fakat
#toplulukların aldığı ödüller olduğu için herhangi bir manipülasyon yapmadım.
empty_rows = df[df['sex'].isnull()]

display(empty_rows)

```


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
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24</th>
      <td>1904</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1904</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>467</td>
      <td>Organization</td>
      <td>Institut de droit international (Institute of ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>60</th>
      <td>1910</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1910</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>477</td>
      <td>Organization</td>
      <td>Bureau international permanent de la Paix (Per...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>89</th>
      <td>1917</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1917</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>482</td>
      <td>Organization</td>
      <td>Comité international de la Croix Rouge (Intern...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>200</th>
      <td>1938</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1938</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>503</td>
      <td>Organization</td>
      <td>Office international Nansen pour les Réfugiés ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>215</th>
      <td>1944</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1944</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>482</td>
      <td>Organization</td>
      <td>Comité international de la Croix Rouge (Intern...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>237</th>
      <td>1947</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1947</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>508</td>
      <td>Organization</td>
      <td>Friends Service Council (The Quakers)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>238</th>
      <td>1947</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1947</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>509</td>
      <td>Organization</td>
      <td>American Friends Service Committee (The Quakers)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>283</th>
      <td>1954</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1954</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>515</td>
      <td>Organization</td>
      <td>Office of the United Nations High Commissioner...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>348</th>
      <td>1963</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1963</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>482</td>
      <td>Organization</td>
      <td>Comité international de la Croix Rouge (Intern...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>349</th>
      <td>1963</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1963</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>523</td>
      <td>Organization</td>
      <td>Ligue des Sociétés de la Croix-Rouge (League o...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>366</th>
      <td>1965</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1965</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>525</td>
      <td>Organization</td>
      <td>United Nations Children's Fund (UNICEF)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>399</th>
      <td>1969</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1969</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>527</td>
      <td>Organization</td>
      <td>International Labour Organization (I.L.O.)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>479</th>
      <td>1977</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1977</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>537</td>
      <td>Organization</td>
      <td>Amnesty International</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>523</th>
      <td>1981</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1981</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>515</td>
      <td>Organization</td>
      <td>Office of the United Nations High Commissioner...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>558</th>
      <td>1985</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1985</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>547</td>
      <td>Organization</td>
      <td>International Physicians for the Prevention of...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>588</th>
      <td>1988</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1988</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>550</td>
      <td>Organization</td>
      <td>United Nations Peacekeeping Forces</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>659</th>
      <td>1995</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1995</td>
      <td>"for their efforts to diminish the part played...</td>
      <td>1/2</td>
      <td>561</td>
      <td>Organization</td>
      <td>Pugwash Conferences on Science and World Affairs</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>682</th>
      <td>1997</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1997</td>
      <td>"for their work for the banning and clearing o...</td>
      <td>1/2</td>
      <td>564</td>
      <td>Organization</td>
      <td>International Campaign to Ban Landmines (ICBL)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>703</th>
      <td>1999</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1999</td>
      <td>"in recognition of the organization's pioneeri...</td>
      <td>1/1</td>
      <td>568</td>
      <td>Organization</td>
      <td>Médecins Sans Frontières</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>729</th>
      <td>2001</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2001</td>
      <td>"for their work for a better organized and mor...</td>
      <td>1/2</td>
      <td>748</td>
      <td>Organization</td>
      <td>United Nations (U.N.)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>778</th>
      <td>2005</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2005</td>
      <td>"for their efforts to prevent nuclear energy f...</td>
      <td>1/2</td>
      <td>797</td>
      <td>Organization</td>
      <td>International Atomic Energy Agency (IAEA)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>789</th>
      <td>2006</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2006</td>
      <td>"for their efforts to create economic and soci...</td>
      <td>1/2</td>
      <td>810</td>
      <td>Organization</td>
      <td>Grameen Bank</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>800</th>
      <td>2007</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2007</td>
      <td>"for their efforts to build up and disseminate...</td>
      <td>1/2</td>
      <td>818</td>
      <td>Organization</td>
      <td>Intergovernmental Panel on Climate Change (IPCC)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>860</th>
      <td>2012</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2012</td>
      <td>"for over six decades contributed to the advan...</td>
      <td>1/1</td>
      <td>881</td>
      <td>Organization</td>
      <td>European Union (EU)</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>873</th>
      <td>2013</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2013</td>
      <td>"for its extensive efforts to eliminate chemic...</td>
      <td>1/1</td>
      <td>893</td>
      <td>Organization</td>
      <td>Organisation for the Prohibition of Chemical W...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>897</th>
      <td>2015</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2015</td>
      <td>"for its decisive contribution to the building...</td>
      <td>1/1</td>
      <td>925</td>
      <td>Organization</td>
      <td>National Dialogue Quartet</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



```python
print(df["year"].dtype)
print(df["year"].head())

```

    int64
    0    1901
    1    1901
    2    1901
    3    1901
    4    1901
    Name: year, dtype: int64
    


```python
df["year"] = pd.to_datetime(df["year"], format='%Y')

```


```python
female_winners = df[df["sex"] == "Female"]
female_winners_sorted = female_winners.sort_values(by="year")
print(female_winners_sorted.head())
```

              year    category                               prize  \
    19  1903-01-01     Physics     The Nobel Prize in Physics 1903   
    29  1905-01-01       Peace          The Nobel Peace Prize 1905   
    51  1909-01-01  Literature  The Nobel Prize in Literature 1909   
    62  1911-01-01   Chemistry   The Nobel Prize in Chemistry 1911   
    128 1926-01-01  Literature  The Nobel Prize in Literature 1926   
    
                                                motivation prize_share  \
    19   "in recognition of the extraordinary services ...         1/4   
    29                                                 NaN         1/1   
    51   "in appreciation of the lofty idealism, vivid ...         1/1   
    62   "in recognition of her services to the advance...         1/1   
    128  "for her idealistically inspired writings whic...         1/1   
    
         laureate_id laureate_type  \
    19             6    Individual   
    29           468    Individual   
    51           579    Individual   
    62             6    Individual   
    128          597    Individual   
    
                                                 full_name  birth_date  \
    19                         Marie Curie, née Sklodowska  1867-11-07   
    29   Baroness Bertha Sophie Felicita von Suttner, n...  1843-06-09   
    51                       Selma Ottilia Lovisa Lagerlöf  1858-11-20   
    62                         Marie Curie, née Sklodowska  1867-11-07   
    128                                     Grazia Deledda  1871-09-27   
    
              birth_city                     birth_country     sex  \
    19            Warsaw           Russian Empire (Poland)  Female   
    29            Prague  Austrian Empire (Czech Republic)  Female   
    51          Mårbacka                            Sweden  Female   
    62            Warsaw           Russian Empire (Poland)  Female   
    128  Nuoro, Sardinia                             Italy  Female   
    
           organization_name organization_city organization_country  death_date  \
    19                   NaN               NaN                  NaN  1934-07-04   
    29                   NaN               NaN                  NaN  1914-06-21   
    51                   NaN               NaN                  NaN  1940-03-16   
    62   Sorbonne University             Paris               France  1934-07-04   
    128                  NaN               NaN                  NaN  1936-08-15   
    
         death_city death_country  
    19   Sallanches        France  
    29       Vienna       Austria  
    51     Mårbacka        Sweden  
    62   Sallanches        France  
    128        Rome         Italy  
    


```python
from IPython.display import display

display(female_winners_sorted.head(10))

```


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
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <td>1903-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1903</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/4</td>
      <td>6</td>
      <td>Individual</td>
      <td>Marie Curie, née Sklodowska</td>
      <td>1867-11-07</td>
      <td>Warsaw</td>
      <td>Russian Empire (Poland)</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1934-07-04</td>
      <td>Sallanches</td>
      <td>France</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1905-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1905</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>468</td>
      <td>Individual</td>
      <td>Baroness Bertha Sophie Felicita von Suttner, n...</td>
      <td>1843-06-09</td>
      <td>Prague</td>
      <td>Austrian Empire (Czech Republic)</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1914-06-21</td>
      <td>Vienna</td>
      <td>Austria</td>
    </tr>
    <tr>
      <th>51</th>
      <td>1909-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1909</td>
      <td>"in appreciation of the lofty idealism, vivid ...</td>
      <td>1/1</td>
      <td>579</td>
      <td>Individual</td>
      <td>Selma Ottilia Lovisa Lagerlöf</td>
      <td>1858-11-20</td>
      <td>Mårbacka</td>
      <td>Sweden</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1940-03-16</td>
      <td>Mårbacka</td>
      <td>Sweden</td>
    </tr>
    <tr>
      <th>62</th>
      <td>1911-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1911</td>
      <td>"in recognition of her services to the advance...</td>
      <td>1/1</td>
      <td>6</td>
      <td>Individual</td>
      <td>Marie Curie, née Sklodowska</td>
      <td>1867-11-07</td>
      <td>Warsaw</td>
      <td>Russian Empire (Poland)</td>
      <td>Female</td>
      <td>Sorbonne University</td>
      <td>Paris</td>
      <td>France</td>
      <td>1934-07-04</td>
      <td>Sallanches</td>
      <td>France</td>
    </tr>
    <tr>
      <th>128</th>
      <td>1926-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1926</td>
      <td>"for her idealistically inspired writings whic...</td>
      <td>1/1</td>
      <td>597</td>
      <td>Individual</td>
      <td>Grazia Deledda</td>
      <td>1871-09-27</td>
      <td>Nuoro, Sardinia</td>
      <td>Italy</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1936-08-15</td>
      <td>Rome</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>141</th>
      <td>1928-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1928</td>
      <td>"principally for her powerful descriptions of ...</td>
      <td>1/1</td>
      <td>601</td>
      <td>Individual</td>
      <td>Sigrid Undset</td>
      <td>1882-05-20</td>
      <td>Kalundborg</td>
      <td>Denmark</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1949-06-10</td>
      <td>Lillehammer</td>
      <td>Norway</td>
    </tr>
    <tr>
      <th>160</th>
      <td>1931-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1931</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>496</td>
      <td>Individual</td>
      <td>Jane Addams</td>
      <td>1860-09-06</td>
      <td>Cedarville, IL</td>
      <td>United States of America</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1935-05-21</td>
      <td>Chicago, IL</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>179</th>
      <td>1935-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1935</td>
      <td>"in recognition of their synthesis of new radi...</td>
      <td>1/2</td>
      <td>194</td>
      <td>Individual</td>
      <td>Irène Joliot-Curie</td>
      <td>1897-09-12</td>
      <td>Paris</td>
      <td>France</td>
      <td>Female</td>
      <td>Institut du Radium</td>
      <td>Paris</td>
      <td>France</td>
      <td>1956-03-17</td>
      <td>Paris</td>
      <td>France</td>
    </tr>
    <tr>
      <th>198</th>
      <td>1938-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1938</td>
      <td>"for her rich and truly epic descriptions of p...</td>
      <td>1/1</td>
      <td>610</td>
      <td>Individual</td>
      <td>Pearl Buck</td>
      <td>1892-06-26</td>
      <td>Hillsboro, WV</td>
      <td>United States of America</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1973-03-06</td>
      <td>Danby, VT</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>218</th>
      <td>1945-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1945</td>
      <td>"for her lyric poetry which, inspired by power...</td>
      <td>1/1</td>
      <td>615</td>
      <td>Individual</td>
      <td>Gabriela Mistral</td>
      <td>1889-04-07</td>
      <td>Vicuña</td>
      <td>Chile</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1957-01-10</td>
      <td>Hempstead, NY</td>
      <td>United States of America</td>
    </tr>
  </tbody>
</table>
</div>


# 3-Nobel Ödüllerini kazanan ilk erkekleri listeleyiniz.



```python
male_winners = df[df["sex"] == "Male"]
male_winners_sorted = male_winners.sort_values(by="year")
print(male_winners_sorted.head())
```

            year    category                                           prize  \
    0 1901-01-01   Chemistry               The Nobel Prize in Chemistry 1901   
    1 1901-01-01  Literature              The Nobel Prize in Literature 1901   
    2 1901-01-01    Medicine  The Nobel Prize in Physiology or Medicine 1901   
    3 1901-01-01       Peace                      The Nobel Peace Prize 1901   
    4 1901-01-01       Peace                      The Nobel Peace Prize 1901   
    
                                              motivation prize_share  laureate_id  \
    0  "in recognition of the extraordinary services ...         1/1          160   
    1  "in special recognition of his poetic composit...         1/1          569   
    2  "for his work on serum therapy, especially its...         1/1          293   
    3                                                NaN         1/2          462   
    4                                                NaN         1/2          463   
    
      laureate_type                     full_name  birth_date         birth_city  \
    0    Individual  Jacobus Henricus van 't Hoff  1852-08-30          Rotterdam   
    1    Individual               Sully Prudhomme  1839-03-16              Paris   
    2    Individual        Emil Adolf von Behring  1854-03-15  Hansdorf (Lawice)   
    3    Individual             Jean Henry Dunant  1828-05-08             Geneva   
    4    Individual                Frédéric Passy  1822-05-20              Paris   
    
          birth_country   sex   organization_name organization_city  \
    0       Netherlands  Male   Berlin University            Berlin   
    1            France  Male                 NaN               NaN   
    2  Prussia (Poland)  Male  Marburg University           Marburg   
    3       Switzerland  Male                 NaN               NaN   
    4            France  Male                 NaN               NaN   
    
      organization_country  death_date death_city death_country  
    0              Germany  1911-03-01     Berlin       Germany  
    1                  NaN  1907-09-07   Châtenay        France  
    2              Germany  1917-03-31    Marburg       Germany  
    3                  NaN  1910-10-30     Heiden   Switzerland  
    4                  NaN  1912-06-12      Paris        France  
    


```python
display(male_winners_sorted.head(10))
```


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
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1901-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1901</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/1</td>
      <td>160</td>
      <td>Individual</td>
      <td>Jacobus Henricus van 't Hoff</td>
      <td>1852-08-30</td>
      <td>Rotterdam</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Berlin University</td>
      <td>Berlin</td>
      <td>Germany</td>
      <td>1911-03-01</td>
      <td>Berlin</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1901-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1901</td>
      <td>"in special recognition of his poetic composit...</td>
      <td>1/1</td>
      <td>569</td>
      <td>Individual</td>
      <td>Sully Prudhomme</td>
      <td>1839-03-16</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1907-09-07</td>
      <td>Châtenay</td>
      <td>France</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1901-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1901</td>
      <td>"for his work on serum therapy, especially its...</td>
      <td>1/1</td>
      <td>293</td>
      <td>Individual</td>
      <td>Emil Adolf von Behring</td>
      <td>1854-03-15</td>
      <td>Hansdorf (Lawice)</td>
      <td>Prussia (Poland)</td>
      <td>Male</td>
      <td>Marburg University</td>
      <td>Marburg</td>
      <td>Germany</td>
      <td>1917-03-31</td>
      <td>Marburg</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1901-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>462</td>
      <td>Individual</td>
      <td>Jean Henry Dunant</td>
      <td>1828-05-08</td>
      <td>Geneva</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1910-10-30</td>
      <td>Heiden</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1901-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>463</td>
      <td>Individual</td>
      <td>Frédéric Passy</td>
      <td>1822-05-20</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1912-06-12</td>
      <td>Paris</td>
      <td>France</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1901-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1901</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/1</td>
      <td>1</td>
      <td>Individual</td>
      <td>Wilhelm Conrad Röntgen</td>
      <td>1845-03-27</td>
      <td>Lennep (Remscheid)</td>
      <td>Prussia (Germany)</td>
      <td>Male</td>
      <td>Munich University</td>
      <td>Munich</td>
      <td>Germany</td>
      <td>1923-02-10</td>
      <td>Munich</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1902-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1902</td>
      <td>"in recognition of the extraordinary service t...</td>
      <td>1/2</td>
      <td>2</td>
      <td>Individual</td>
      <td>Hendrik Antoon Lorentz</td>
      <td>1853-07-18</td>
      <td>Arnhem</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Leiden University</td>
      <td>Leiden</td>
      <td>Netherlands</td>
      <td>1928-02-04</td>
      <td>NaN</td>
      <td>Netherlands</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1902-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1902</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>465</td>
      <td>Individual</td>
      <td>Charles Albert Gobat</td>
      <td>1843-05-21</td>
      <td>Tramelan</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1914-03-16</td>
      <td>Bern</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1902-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1902</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>464</td>
      <td>Individual</td>
      <td>Élie Ducommun</td>
      <td>1833-02-19</td>
      <td>Geneva</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1906-12-07</td>
      <td>Bern</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1902-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1902</td>
      <td>"in recognition of the extraordinary service t...</td>
      <td>1/2</td>
      <td>3</td>
      <td>Individual</td>
      <td>Pieter Zeeman</td>
      <td>1865-05-25</td>
      <td>Zonnemaire</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Amsterdam University</td>
      <td>Amsterdam</td>
      <td>Netherlands</td>
      <td>1943-10-09</td>
      <td>Amsterdam</td>
      <td>Netherlands</td>
    </tr>
  </tbody>
</table>
</div>


# 4-Nobel ödülünü en çok kazanan ülkenin hangi yıldan itibaren hakimiyet sağladığını görselleştirip bu hakimiyette rol oynayan şeyler nelerdir? İçgörülerinizi paylaşır mısınız?


```python
en_cok= df['birth_country'].value_counts().head(1)

print(en_cok)
```

    birth_country
    United States of America    259
    Name: count, dtype: int64
    


```python
usa="United States of America"
```


```python
yıllar = df[df['birth_country'] == usa]
```


```python
yıllar.head(40)
```




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
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>35</th>
      <td>1906-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1906</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>470</td>
      <td>Individual</td>
      <td>Theodore Roosevelt</td>
      <td>1858-10-27</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1919-01-06</td>
      <td>Oyster Bay, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>72</th>
      <td>1912-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1912</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>480</td>
      <td>Individual</td>
      <td>Elihu Root</td>
      <td>1845-02-15</td>
      <td>Clinton, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1937-02-07</td>
      <td>New York, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>79</th>
      <td>1914-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1914</td>
      <td>"in recognition of his accurate determinations...</td>
      <td>1/1</td>
      <td>175</td>
      <td>Individual</td>
      <td>Theodore William Richards</td>
      <td>1868-01-31</td>
      <td>Germantown, PA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Harvard University</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
      <td>1928-04-02</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>95</th>
      <td>1919-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1919</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>483</td>
      <td>Individual</td>
      <td>Thomas Woodrow Wilson</td>
      <td>1856-12-28</td>
      <td>Staunton, VA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1924-02-03</td>
      <td>Washington, DC</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>117</th>
      <td>1923-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1923</td>
      <td>"for his work on the elementary charge of elec...</td>
      <td>1/1</td>
      <td>28</td>
      <td>Individual</td>
      <td>Robert Andrews Millikan</td>
      <td>1868-03-22</td>
      <td>Morrison, IL</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>California Institute of Technology (Caltech)</td>
      <td>Pasadena, CA</td>
      <td>United States of America</td>
      <td>1953-12-19</td>
      <td>San Marino, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>124</th>
      <td>1925-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1925</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>489</td>
      <td>Individual</td>
      <td>Charles Gates Dawes</td>
      <td>1865-08-27</td>
      <td>Marietta, OH</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1951-04-23</td>
      <td>Evanston, IL</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>138</th>
      <td>1927-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1927</td>
      <td>"for his discovery of the effect named after him"</td>
      <td>1/2</td>
      <td>33</td>
      <td>Individual</td>
      <td>Arthur Holly Compton</td>
      <td>1892-09-10</td>
      <td>Wooster, OH</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>University of Chicago</td>
      <td>Chicago, IL</td>
      <td>United States of America</td>
      <td>1962-03-15</td>
      <td>Berkeley, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>149</th>
      <td>1929-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1929</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>494</td>
      <td>Individual</td>
      <td>Frank Billings Kellogg</td>
      <td>1856-12-22</td>
      <td>Potsdam, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1937-12-21</td>
      <td>St. Paul, MN</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>152</th>
      <td>1930-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1930</td>
      <td>"for his vigorous and graphic art of descripti...</td>
      <td>1/1</td>
      <td>603</td>
      <td>Individual</td>
      <td>Sinclair Lewis</td>
      <td>1885-02-07</td>
      <td>Sauk Centre, MN</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1951-01-10</td>
      <td>Rome</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>160</th>
      <td>1931-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1931</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>496</td>
      <td>Individual</td>
      <td>Jane Addams</td>
      <td>1860-09-06</td>
      <td>Cedarville, IL</td>
      <td>United States of America</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1935-05-21</td>
      <td>Chicago, IL</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>161</th>
      <td>1931-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1931</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>497</td>
      <td>Individual</td>
      <td>Nicholas Murray Butler</td>
      <td>1862-04-02</td>
      <td>Elizabeth, NJ</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Columbia University</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>1947-12-07</td>
      <td>New York, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>162</th>
      <td>1932-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1932</td>
      <td>"for his discoveries and investigations in sur...</td>
      <td>1/1</td>
      <td>191</td>
      <td>Individual</td>
      <td>Irving Langmuir</td>
      <td>1881-01-31</td>
      <td>Brooklyn, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>General Electric Company</td>
      <td>Schenectady, NY</td>
      <td>United States of America</td>
      <td>1957-08-16</td>
      <td>Falmouth, MA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>168</th>
      <td>1933-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1933</td>
      <td>"for his discoveries concerning the role playe...</td>
      <td>1/1</td>
      <td>325</td>
      <td>Individual</td>
      <td>Thomas Hunt Morgan</td>
      <td>1866-09-25</td>
      <td>Lexington, KY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>California Institute of Technology (Caltech)</td>
      <td>Pasadena, CA</td>
      <td>United States of America</td>
      <td>1945-12-04</td>
      <td>Pasadena, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>172</th>
      <td>1934-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1934</td>
      <td>"for his discovery of heavy hydrogen"</td>
      <td>1/1</td>
      <td>192</td>
      <td>Individual</td>
      <td>Harold Clayton Urey</td>
      <td>1893-04-29</td>
      <td>Walkerton, IN</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Columbia University</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>1981-01-05</td>
      <td>La Jolla, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>174</th>
      <td>1934-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1934</td>
      <td>"for their discoveries concerning liver therap...</td>
      <td>1/3</td>
      <td>326</td>
      <td>Individual</td>
      <td>George Hoyt Whipple</td>
      <td>1878-08-28</td>
      <td>Ashland, NH</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>University of Rochester</td>
      <td>Rochester, NY</td>
      <td>United States of America</td>
      <td>1976-02-01</td>
      <td>Rochester, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>175</th>
      <td>1934-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1934</td>
      <td>"for their discoveries concerning liver therap...</td>
      <td>1/3</td>
      <td>327</td>
      <td>Individual</td>
      <td>George Richards Minot</td>
      <td>1885-12-02</td>
      <td>Boston, MA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Harvard University</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
      <td>1950-02-25</td>
      <td>Brookline, MA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>176</th>
      <td>1934-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1934</td>
      <td>"for their discoveries concerning liver therap...</td>
      <td>1/3</td>
      <td>328</td>
      <td>Individual</td>
      <td>William Parry Murphy</td>
      <td>1892-02-06</td>
      <td>Stoughton, WI</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Harvard University</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
      <td>1987-10-09</td>
      <td>Brookline, MA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>184</th>
      <td>1936-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1936</td>
      <td>"for the power, honesty and deep-felt emotions...</td>
      <td>1/1</td>
      <td>608</td>
      <td>Individual</td>
      <td>Eugene Gladstone O'Neill</td>
      <td>1888-10-16</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1953-11-27</td>
      <td>Boston, MA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>189</th>
      <td>1936-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1936</td>
      <td>"for his discovery of the positron"</td>
      <td>1/2</td>
      <td>43</td>
      <td>Individual</td>
      <td>Carl David Anderson</td>
      <td>1905-09-03</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>California Institute of Technology (Caltech)</td>
      <td>Pasadena, CA</td>
      <td>United States of America</td>
      <td>1991-01-11</td>
      <td>San Marino, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>195</th>
      <td>1937-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1937</td>
      <td>"for their experimental discovery of the diffr...</td>
      <td>1/2</td>
      <td>44</td>
      <td>Individual</td>
      <td>Clinton Joseph Davisson</td>
      <td>1881-10-22</td>
      <td>Bloomington, IL</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Bell Telephone Laboratories</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>1958-02-01</td>
      <td>Charlottesville, VA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>198</th>
      <td>1938-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1938</td>
      <td>"for her rich and truly epic descriptions of p...</td>
      <td>1/1</td>
      <td>610</td>
      <td>Individual</td>
      <td>Pearl Buck</td>
      <td>1892-06-26</td>
      <td>Hillsboro, WV</td>
      <td>United States of America</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1973-03-06</td>
      <td>Danby, VT</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>206</th>
      <td>1939-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1939</td>
      <td>"for the invention and development of the cycl...</td>
      <td>1/1</td>
      <td>47</td>
      <td>Individual</td>
      <td>Ernest Orlando Lawrence</td>
      <td>1901-08-08</td>
      <td>Canton, SD</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>University of California</td>
      <td>Berkeley, CA</td>
      <td>United States of America</td>
      <td>1958-08-27</td>
      <td>Palo Alto, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>209</th>
      <td>1943-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1943</td>
      <td>"for his discovery of the chemical nature of v...</td>
      <td>1/2</td>
      <td>336</td>
      <td>Individual</td>
      <td>Edward Adelbert Doisy</td>
      <td>1893-11-13</td>
      <td>Hume, IL</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Saint Louis University</td>
      <td>St. Louis, MO</td>
      <td>United States of America</td>
      <td>1986-10-23</td>
      <td>St. Louis, MO</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>213</th>
      <td>1944-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1944</td>
      <td>"for their discoveries relating to the highly ...</td>
      <td>1/2</td>
      <td>337</td>
      <td>Individual</td>
      <td>Joseph Erlanger</td>
      <td>1874-01-05</td>
      <td>San Francisco, CA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Washington University</td>
      <td>St. Louis, MO</td>
      <td>United States of America</td>
      <td>1965-12-05</td>
      <td>St. Louis, MO</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>214</th>
      <td>1944-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1944</td>
      <td>"for their discoveries relating to the highly ...</td>
      <td>1/2</td>
      <td>338</td>
      <td>Individual</td>
      <td>Herbert Spencer Gasser</td>
      <td>1888-07-05</td>
      <td>Platteville, WI</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Rockefeller Institute for Medical Research</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>1963-05-11</td>
      <td>New York, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>222</th>
      <td>1945-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1945</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>505</td>
      <td>Individual</td>
      <td>Cordell Hull</td>
      <td>1871-10-02</td>
      <td>Olympus, TN</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1955-07-23</td>
      <td>Bethesda, MD</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>224</th>
      <td>1946-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1946</td>
      <td>"for his discovery that enzymes can be crystal...</td>
      <td>1/2</td>
      <td>204</td>
      <td>Individual</td>
      <td>James Batcheller Sumner</td>
      <td>1887-11-19</td>
      <td>Canton, MA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Cornell University</td>
      <td>Ithaca, NY</td>
      <td>United States of America</td>
      <td>1955-08-12</td>
      <td>Buffalo, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>225</th>
      <td>1946-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1946</td>
      <td>"for their preparation of enzymes and virus pr...</td>
      <td>1/4</td>
      <td>205</td>
      <td>Individual</td>
      <td>John Howard Northrop</td>
      <td>1891-07-05</td>
      <td>Yonkers, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Rockefeller Institute for Medical Research</td>
      <td>Princeton, NJ</td>
      <td>United States of America</td>
      <td>1987-05-27</td>
      <td>Wickenberg, AZ</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>226</th>
      <td>1946-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1946</td>
      <td>"for their preparation of enzymes and virus pr...</td>
      <td>1/4</td>
      <td>206</td>
      <td>Individual</td>
      <td>Wendell Meredith Stanley</td>
      <td>1904-08-16</td>
      <td>Ridgeville, IN</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Rockefeller Institute for Medical Research</td>
      <td>Princeton, NJ</td>
      <td>United States of America</td>
      <td>1971-06-15</td>
      <td>Salamanca</td>
      <td>Spain</td>
    </tr>
    <tr>
      <th>228</th>
      <td>1946-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1946</td>
      <td>"for the discovery of the production of mutati...</td>
      <td>1/1</td>
      <td>342</td>
      <td>Individual</td>
      <td>Hermann Joseph Muller</td>
      <td>1890-12-21</td>
      <td>New York, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Indiana University</td>
      <td>Bloomington, IN</td>
      <td>United States of America</td>
      <td>1967-04-05</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>229</th>
      <td>1946-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1946</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>506</td>
      <td>Individual</td>
      <td>Emily Greene Balch</td>
      <td>1867-01-08</td>
      <td>Jamaica Plain, MA (Boston)</td>
      <td>United States of America</td>
      <td>Female</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1961-01-09</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>230</th>
      <td>1946-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1946</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>507</td>
      <td>Individual</td>
      <td>John Raleigh Mott</td>
      <td>1865-05-25</td>
      <td>Livingston Manor, NY</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1955-01-31</td>
      <td>NaN</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>231</th>
      <td>1946-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 1946</td>
      <td>"for the invention of an apparatus to produce ...</td>
      <td>1/1</td>
      <td>51</td>
      <td>Individual</td>
      <td>Percy Williams Bridgman</td>
      <td>1882-04-21</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Harvard University</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
      <td>1961-08-20</td>
      <td>Randolph, NH</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>241</th>
      <td>1948-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1948</td>
      <td>"for his outstanding, pioneer contribution to ...</td>
      <td>1/1</td>
      <td>619</td>
      <td>Individual</td>
      <td>Thomas Stearns Eliot</td>
      <td>1888-09-26</td>
      <td>St. Louis, MO</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1965-01-04</td>
      <td>London</td>
      <td>United Kingdom</td>
    </tr>
    <tr>
      <th>245</th>
      <td>1949-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1949</td>
      <td>"for his powerful and artistically unique cont...</td>
      <td>1/1</td>
      <td>620</td>
      <td>Individual</td>
      <td>William Faulkner</td>
      <td>1897-09-25</td>
      <td>New Albany, MS</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1962-07-06</td>
      <td>Byhalia, MS</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>253</th>
      <td>1950-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1950</td>
      <td>"for their discoveries relating to the hormone...</td>
      <td>1/3</td>
      <td>349</td>
      <td>Individual</td>
      <td>Edward Calvin Kendall</td>
      <td>1886-03-08</td>
      <td>South Norwalk, CT</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Mayo Clinic</td>
      <td>Rochester, MN</td>
      <td>United States of America</td>
      <td>1972-05-04</td>
      <td>Princeton, NJ</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>255</th>
      <td>1950-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1950</td>
      <td>"for their discoveries relating to the hormone...</td>
      <td>1/3</td>
      <td>351</td>
      <td>Individual</td>
      <td>Philip Showalter Hench</td>
      <td>1896-02-28</td>
      <td>Pittsburgh, PA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Mayo Clinic</td>
      <td>Rochester, MN</td>
      <td>United States of America</td>
      <td>1965-03-30</td>
      <td>Ocho Rios</td>
      <td>Jamaica</td>
    </tr>
    <tr>
      <th>256</th>
      <td>1950-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1950</td>
      <td>NaN</td>
      <td>1/1</td>
      <td>511</td>
      <td>Individual</td>
      <td>Ralph Bunche</td>
      <td>1904-08-07</td>
      <td>Detroit, MI</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>Harvard University</td>
      <td>Cambridge, MA</td>
      <td>United States of America</td>
      <td>1971-12-09</td>
      <td>New York, NY</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>258</th>
      <td>1951-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1951</td>
      <td>"for their discoveries in the chemistry of the...</td>
      <td>1/2</td>
      <td>212</td>
      <td>Individual</td>
      <td>Edwin Mattison McMillan</td>
      <td>1907-09-18</td>
      <td>Redondo Beach, CA</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>University of California</td>
      <td>Berkeley, CA</td>
      <td>United States of America</td>
      <td>1991-09-07</td>
      <td>El Cerrito, CA</td>
      <td>United States of America</td>
    </tr>
    <tr>
      <th>259</th>
      <td>1951-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1951</td>
      <td>"for their discoveries in the chemistry of the...</td>
      <td>1/2</td>
      <td>213</td>
      <td>Individual</td>
      <td>Glenn Theodore Seaborg</td>
      <td>1912-04-19</td>
      <td>Ishpeming, MI</td>
      <td>United States of America</td>
      <td>Male</td>
      <td>University of California</td>
      <td>Berkeley, CA</td>
      <td>United States of America</td>
      <td>1999-02-25</td>
      <td>Lafayette, CA</td>
      <td>United States of America</td>
    </tr>
  </tbody>
</table>
</div>




```python
odul_alinan_yillar = yıllar['year'].dt.year
```


```python
odul_alinan_yillar
```




    35     1906
    72     1912
    79     1914
    95     1919
    117    1923
           ... 
    876    2014
    878    2014
    881    2014
    890    2015
    905    2016
    Name: year, Length: 259, dtype: int32




```python
odul_sayilari = odul_alinan_yillar.value_counts().sort_index()
odul_sayilari
```




    year
    1906    1
    1912    1
    1914    1
    1919    1
    1923    1
           ..
    2012    5
    2013    5
    2014    3
    2015    1
    2016    1
    Name: count, Length: 85, dtype: int64




```python
plt.figure(figsize=(13, 6))
sns.lineplot(x=odul_sayilari.index, y=odul_sayilari.values, color='tan', marker='o', markersize=8, markerfacecolor='gray')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title(f'USA Ülkesinin Yıllara Göre Nobel Ödülü Kazanma Sayısı')
plt.grid(axis='y', linestyle='--', alpha=0.7)
for i, txt in enumerate(odul_sayilari.values):
    plt.text(odul_sayilari.index[i], txt, odul_sayilari.index[i], ha='center', va='bottom', fontsize=9, color='black', rotation=70)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

```


    
![png](output_31_0.png)
    



```python
categories = df['category'].unique()

for category in categories:
    filtered_data = df[(df['category'] == category) & (df['birth_country'] == 'United States of America')]

    plt.figure(figsize=(12, 8))
    sns.scatterplot(data=filtered_data, x='year', y='birth_date', hue='sex', style='sex', palette='Set2', s=100)
    plt.title(f'USA {category} Nobel Ödülü Kazananların Cinsiyet ve Yaşları')
    plt.xlabel('Yıl')
    plt.ylabel('Yaş')
    plt.legend(title='Cinsiyet', loc='upper left')
    plt.grid(True)
    plt.show()



```


    
![png](output_32_0.png)
    



    
![png](output_32_1.png)
    



    
![png](output_32_2.png)
    



    
![png](output_32_3.png)
    



    
![png](output_32_4.png)
    



    
![png](output_32_5.png)
    


# 5-Nobel Ödülü kazananların cinsiyetlerini, yaşlarını, ödül kategorisi ve yılları kullanarak görselleştiriniz.(Her bir ödül kategorisi için ayrı grafik gösteriniz) Çıkan sonuçlara göre görseli yorumlayınız.


```python
df
```




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
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1901-01-01</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1901</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/1</td>
      <td>160</td>
      <td>Individual</td>
      <td>Jacobus Henricus van 't Hoff</td>
      <td>1852-08-30</td>
      <td>Rotterdam</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Berlin University</td>
      <td>Berlin</td>
      <td>Germany</td>
      <td>1911-03-01</td>
      <td>Berlin</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1901-01-01</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1901</td>
      <td>"in special recognition of his poetic composit...</td>
      <td>1/1</td>
      <td>569</td>
      <td>Individual</td>
      <td>Sully Prudhomme</td>
      <td>1839-03-16</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1907-09-07</td>
      <td>Châtenay</td>
      <td>France</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1901-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1901</td>
      <td>"for his work on serum therapy, especially its...</td>
      <td>1/1</td>
      <td>293</td>
      <td>Individual</td>
      <td>Emil Adolf von Behring</td>
      <td>1854-03-15</td>
      <td>Hansdorf (Lawice)</td>
      <td>Prussia (Poland)</td>
      <td>Male</td>
      <td>Marburg University</td>
      <td>Marburg</td>
      <td>Germany</td>
      <td>1917-03-31</td>
      <td>Marburg</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1901-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>462</td>
      <td>Individual</td>
      <td>Jean Henry Dunant</td>
      <td>1828-05-08</td>
      <td>Geneva</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1910-10-30</td>
      <td>Heiden</td>
      <td>Switzerland</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1901-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>463</td>
      <td>Individual</td>
      <td>Frédéric Passy</td>
      <td>1822-05-20</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1912-06-12</td>
      <td>Paris</td>
      <td>France</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>906</th>
      <td>2016-01-01</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 2016</td>
      <td>"for his discoveries of mechanisms for autophagy"</td>
      <td>1/1</td>
      <td>927</td>
      <td>Individual</td>
      <td>Yoshinori Ohsumi</td>
      <td>1945-02-09</td>
      <td>Fukuoka</td>
      <td>Japan</td>
      <td>Male</td>
      <td>Tokyo Institute of Technology</td>
      <td>Tokyo</td>
      <td>Japan</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>907</th>
      <td>2016-01-01</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 2016</td>
      <td>"for his resolute efforts to bring the country...</td>
      <td>1/1</td>
      <td>934</td>
      <td>Individual</td>
      <td>Juan Manuel Santos</td>
      <td>1951-08-10</td>
      <td>Bogotá</td>
      <td>Colombia</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>908</th>
      <td>2016-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 2016</td>
      <td>"for theoretical discoveries of topological ph...</td>
      <td>1/2</td>
      <td>928</td>
      <td>Individual</td>
      <td>David J. Thouless</td>
      <td>1934-09-21</td>
      <td>Bearsden</td>
      <td>United Kingdom</td>
      <td>Male</td>
      <td>University of Washington</td>
      <td>Seattle, WA</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>909</th>
      <td>2016-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 2016</td>
      <td>"for theoretical discoveries of topological ph...</td>
      <td>1/4</td>
      <td>929</td>
      <td>Individual</td>
      <td>F. Duncan M. Haldane</td>
      <td>1951-09-14</td>
      <td>London</td>
      <td>United Kingdom</td>
      <td>Male</td>
      <td>Princeton University</td>
      <td>Princeton, NJ</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>910</th>
      <td>2016-01-01</td>
      <td>Physics</td>
      <td>The Nobel Prize in Physics 2016</td>
      <td>"for theoretical discoveries of topological ph...</td>
      <td>1/4</td>
      <td>930</td>
      <td>Individual</td>
      <td>J. Michael Kosterlitz</td>
      <td>1943-06-22</td>
      <td>Aberdeen</td>
      <td>United Kingdom</td>
      <td>Male</td>
      <td>Brown University</td>
      <td>Providence, RI</td>
      <td>United States of America</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>911 rows × 18 columns</p>
</div>




```python
print(df['birth_date'].dtype)
```

    object
    


```python
df['birth_date'] = pd.to_datetime(df['birth_date'])
```


```python
print(df['year'].dtype)
```

    datetime64[ns]
    


```python
df['year'] = pd.to_datetime(df['year'], format='%Y')

```


```python
df['award_year'] = df['year'].dt.year
```


```python
df['birth_year'] = df['birth_date'].dt.year
```


```python
type('award_year')
```




    str




```python
df.isnull().sum()
```




    year                      0
    category                  0
    prize                     0
    motivation               88
    prize_share               0
    laureate_id               0
    laureate_type             0
    full_name                 0
    birth_date               28
    birth_city               28
    birth_country            26
    sex                      26
    organization_name       246
    organization_city       244
    organization_country    244
    death_date              318
    death_city              335
    death_country           329
    award_year                0
    birth_year               28
    dtype: int64




```python
df['age'] = df['award_year'] - df['birth_year']
```


```python
df['age'].unique()
```




    array([49., 62., 47., 73., 79., 56., 50., 85., 45., 69., 59., 37., 44.,
           71., 43., 75., 51., 36., 52., 74., 72., 55., nan, 70., 54., 63.,
           48., 42., 64., 68., 80., 57., 35., 41., 58., 39., 67., 60., 46.,
           38., 53., 25., 40., 61., 77., 32., 86., 65., 31., 66., 81., 78.,
           33., 34., 87., 76., 84., 82., 83., 88., 90., 89., 17.])




```python
df.loc[df['age'] > 999, 'age'] = 0
```


```python
df['age'].unique()
```




    array([49., 62., 47., 73., 79., 56., 50., 85., 45., 69., 59., 37., 44.,
           71., 43., 75., 51., 36., 52., 74., 72., 55., nan, 70., 54., 63.,
           48., 42., 64., 68., 80., 57., 35., 41., 58., 39., 67., 60., 46.,
           38., 53., 25., 40., 61., 77., 32., 86., 65., 31., 66., 81., 78.,
           33., 34., 87., 76., 84., 82., 83., 88., 90., 89., 17.])




```python
df['birth_year'] = df['birth_year'].fillna(0).astype(int)
```


```python
df.isnull().sum()
```




    year                      0
    category                  0
    prize                     0
    motivation               88
    prize_share               0
    laureate_id               0
    laureate_type             0
    full_name                 0
    birth_date               28
    birth_city               28
    birth_country            26
    sex                      26
    organization_name       246
    organization_city       244
    organization_country    244
    death_date              318
    death_city              335
    death_country           329
    award_year                0
    birth_year                0
    age                      28
    dtype: int64




```python

def plot_award_category(df, category):
    df_category = df[df['category'] == category]
    
    plt.figure(figsize=(10, 6))
    sns.scatterplot(data=df_category, x='year', y='age', hue='sex', style='sex', palette='Set2', s=100)
    plt.title(f'{category} Ödülü Kazananların Cinsiyet ve Yaşları')
    plt.xlabel('Yıl')
    plt.ylabel('Yaş')
    plt.legend(title='Cinsiyet', loc='upper left')
    plt.grid(True)
    plt.show()

for category in df['category'].unique():
    plot_award_category(df, category)



```


    
![png](output_49_0.png)
    



    
![png](output_49_1.png)
    



    
![png](output_49_2.png)
    



    
![png](output_49_3.png)
    



    
![png](output_49_4.png)
    



    
![png](output_49_5.png)
    


# 6-1938-1945 yılı arasında Nobel Ödülü kazananların kategorilerini ve ülkelerini görselleştirip yorumlayınız.


```python

df_1938_1945 = df[(df['year'] >= '1938-01-01') & (df['year'] <= '1945-12-31')]

grouped_data = df_1938_1945.groupby(['category', 'birth_country']).size().reset_index(name='count')


plt.figure(figsize=(10, 8))
sns.barplot(data=grouped_data, x='count', y='birth_country', hue='category', palette='Set2' )
plt.title('1938-1945 Yılları Arasında Nobel Ödülü Alanların Kategorilere ve Ülkelere Göre Dağılımı')
plt.xlabel('Kazanan Sayısı')
plt.ylabel('Ülke')
plt.legend(title='Kategori', loc='upper right')
plt.grid(True, axis='x')
plt.show()




```


    
![png](output_51_0.png)
    


# 7-1947-1991 yılları arasında Nobel Ödülü kazananların kategorilerini ve ülkelerini görselleştirip yorumlayınız.(Her kategori için ayrı bir grafik olması istenmektedir)


```python

df_1947_1991 = df[(df['year'] >= '1947-01-01') & (df['year'] <= '1991-12-31')]

def plot_award_category(ax, df, category):

    df_category = df[df['category'] == category]
    
    grouped_data = df_category.groupby(['category', 'birth_country']).size().reset_index(name='count')
    
    sns.barplot(data=grouped_data, x='count', y='birth_country', palette='Set2', ax=ax)
    ax.set_title(f'{category} Ödülü Kazananların Ülkelere Göre Dağılımı (1947-1991)')
    ax.set_xlabel('Kazanan Sayısı')
    ax.set_ylabel('Ülke')
    ax.grid(True, axis='x')

fig, axes = plt.subplots(nrows=3, ncols=2, figsize=(15, 15))

for idx, category in enumerate(df['category'].unique()):
    plot_award_category(axes[idx//2, idx%2], df_1947_1991, category)

plt.tight_layout()
plt.show()

```


    
![png](output_53_0.png)
    



```python

filtered_data = df[(df['year'] >= '1947-01-01') & (df['year'] <= '1991-12-31')]

categories = filtered_data['category'].unique()
for category in categories:
    plt.figure(figsize=(12, 6))
    ax = sns.countplot(data=filtered_data[filtered_data['category'] == category], x='birth_country', palette='Set2')
    plt.title(f'{category} Ödülü Kazananların Ülkelerine Göre Dağılımı (1947-1991)')
    plt.xlabel('Ülke')
    plt.xticks(rotation=90)  
    
    for p in ax.patches:
        ax.annotate(f'{int(p.get_height())}', (p.get_x() + p.get_width() / 2., p.get_height()), 
                    ha='center', va='center', fontsize=10, color='black', xytext=(0, 5), 
                    textcoords='offset points')

    plt.gca().axes.get_yaxis().set_visible(False)  
    plt.grid(axis='y', linestyle='--', alpha=0.7)
    plt.tight_layout()
    plt.show()

```


    
![png](output_54_0.png)
    



    
![png](output_54_1.png)
    



    
![png](output_54_2.png)
    



    
![png](output_54_3.png)
    



    
![png](output_54_4.png)
    



    
![png](output_54_5.png)
    


# 8-Kimya, Edebiyat, Barış, Fizik ve Tıp kategorilerindeki 2000 sonrasındaki kişilerin ülkelerini, yaşlarını görselleştirin.(Her bir Kategori için ayrı görselleştirme yapılması istenmektedir) Veriyi yorumlayınız.


```python

filtered_data = df[(df['year'] >= '2000-01-01') & 
                   (df['category'].isin(['Chemistry', 'Literature', 'Peace', 'Physics', 'Medicine']))]

categories = filtered_data['category'].unique()
for category in categories:
    plt.figure(figsize=(10, 6))
    sns.scatterplot(data=filtered_data[filtered_data['category'] == category], x='birth_country', y='age', 
                    hue='sex', palette='Set2', s=100)
    plt.title(f'{category} Kategorisindeki Nobel Ödülü Kazananların Ülke ve Yaş Dağılımı (2000 sonrası)')
    plt.xlabel('Ülke')
    plt.ylabel('Yaş')
    plt.xticks(rotation=90) 
    plt.legend(title='Cinsiyet', loc='upper right')
    plt.grid(True)
    plt.tight_layout()
    plt.show()

```


    
![png](output_56_0.png)
    



    
![png](output_56_1.png)
    



    
![png](output_56_2.png)
    



    
![png](output_56_3.png)
    



    
![png](output_56_4.png)
    


#                                               TEŞEKKÜRLER


```python

```


```python

```


```python

```


```python

```
