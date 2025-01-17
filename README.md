### Create ERD diagram from pandas dataframes
* create an ERD object and add tables and connections between tables
* save the generated dot code to an `output.txt` file containing 
* copy-paste the `output.txt` into a graphviz rendering tool like this [one](https://edotor.net/) 
* the output image at the bottom is generated by using the above link 

###
Installation via pip:
```
pip install pandaserd
```

Example use:
```
import pandas as pd
from pandaserd import ERD

df1 = pd.DataFrame(data=[[123, 32, '1 Ottawa Street'], [123, 80, '14 Canada Road']])
df1.columns = ['PERSON', 'AGE', 'ADDRESS']
df2 = pd.DataFrame(data=[[6342, 124123124124, '1992-01-02', 21, 'K012V4'], [3124, 154823124124, '1984-02-02',42,'L4Y6S2']])
df2.columns = ['PERSON', 'CREDIT_CARD', 'DOB', 'PERSON_AGE', 'POSTAL_CODE']

erd = ERD()
t1 = erd.add_table(df1, 'PERSON', bg_color='pink')
t2 = erd.add_table(df2, 'CREDIT_CARD', bg_color='skyblue')
erd.create_rel('PERSON', 'CREDIT_CARD', on='PERSON', right_cardinality='*')
erd.create_rel('PERSON', 'CREDIT_CARD', left_on='AGE', right_on='PERSON_AGE', left_cardinality='+', right_cardinality='+')

erd.write_to_file('output.txt')

```
![example image](example_erd.png "Title")

Color names (e.g. "pink" and "skyblue" above) follow [standard 140 HTML named colors](https://www.w3schools.com/colors/colors_names.asp). 

### Credits
Largely inspired by this fab [repo](https://github.com/ehne/ERDot)!
* dot documentation can be found [here](https://www.graphviz.org/pdf/dotguide.pdf)
