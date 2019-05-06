# Open Welfare Data Brazil

Collects municipal-level data from Several Brazilian Government's Social Programs.

Collects data from Public API's that contains information related to the following programs:
- Bolsa Familia Program  **OK**
- PETI (Slave Labour Erradication Program)  **OK**
- Seguro Defeso  *Soon*
- FIES (Financiamento Estudantil)  *Soon*
- PROUNI  *Soon*

## Introduction:
The package has some simple functions that needs to be understood by the user. Only with that knowledge of these, one can make a good use of it. All these functions were written in a way to support multiple requests at once, in order to facilitate the download of data from multiple municipalities.

#### **``uflist()`` function** 

The first step in using the package is running the ``uflist()`` function, this function takes **no arguments** and it returns a tibble with three columns: the first one is the ``num``(with the numeric identifier of the State); the second one being the ``EST`` column, with the full name of the State; and the last one, the ``UF`` column, which contains the UF code, that is a short name (abbreviation?) for a State.

#### **``munlist()`` function**

Then, having the list of the States, one should run the ``num`` of the desired state(s) inside the munlist() function. It's going to request the list of all the municipalities in the desired State and then it will return them in a tibble object. (Why a tibble? Click [here](https://www.r-bloggers.com/a-tour-of-the-tibble-package/).

This list is needed because each municipality has a unique identifier, and this one is needed to request municipal-level data from Government's APIs.

use: ``help(munlist)`` to get the meaning of each column in the tibble returned by the function. 
#### **``get[program]_mun`` function family**

Finally, to request the data, one should run the ``get(pbf/peti)_mun()`` function in those numbers that are in the ``codigo_municipio`` column that was generated by the ``munlist()`` function.

##### Example
In the above example we are going to collect *Bolsa Familia Program* data from all municipaities in the state of Rondônia.

``
states <- uflist()

View(states)
``

In the generated tibble, we can see that the ``num`` of the State of Rondônia is 11, so if we plan to collect data from this State, one should do the following:

``
munis <- munlist(11)
``

Then, after a few seconds, the tibble with the list of municipalities in the state of Rondônia is return, and then finally we can get the desired data using the code:

``
data.pbf <- getpbf_mun(munis$codigo_municipio)
``

And that's it.
