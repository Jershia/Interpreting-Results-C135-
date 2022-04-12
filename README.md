# Interpreting Results
## Steps To Find suitable planets For Survival
  * *In the last class, we came up with a dictionary containing all the planets and a list of their features (gravity, type, goldilock and speed), whether it supports it or not.*
  * *Find out the number of planets that have gravity listed as one of the features **(Code is given below)**.The count comes out to be 3,951. This is exactly the same as the number of planets we found out to have suitable gravity* 
  * *Find out the number of planets that have planet_type listed as one of the features  **(Code is given below)**.Here, the count comes out to be 1,485 while we earlier got 1,452 when we found out the number of planets that are either Terrestrial or Super Earth like. That’s because there are planets that do not support gravity but are of suitable types. Earlier, we only checked the type of planets that supported gravity.*
  * *We got the count for planets that do not support gravity but are of suitable type 33.If we subtract 33 from 1,485, we get 1,452 which matches with our findings earlier.*
  * *Find the number of planets that are in the goldilock zone and have suitable speed in the dictionary.we remember to make a few changes in columns. We are not
performing any changes to any of the columns this time when we are creating a dictionary. We also did not handle Unknown values this time*
  * *We are trying to add goldilock features to planets that are in the Goldilock zone, but it's in X AU format and we are not handling that. We have to split the string from a <space>, take the first element and convert it to float.**(Code is given below)**.*
  * *We also have to fix the speed calculation. Again, we will fix the distance by converting it to float after we split it and we also have to convert orbital_period to days.**(Code is given below)**.*
  * *Now, our planets in the Goldilock zone were 25 and the planets that had suitable speed was 8. These planets also exhibited the properties of suitable gravity and
planet type. Find out all such planets that exhibit all the properties.*
  * *Here, the result is 0 for both of them. This does not match with the analysis result that we got earlier.To debug this, remove the try-except statements from the code where we are adding goldilock and speed properties and see what errors we are getting. It now says that float object has no attribute lower. This means that there might be some values that are float. Fix this by handling these situations.*
  * *Re-run the blocks that gave us the output 0 and 0 for planets supporting all the properties and this time, we shall get 25 for goldilock planets and 6 for planets with both goldilock and speed.*
 
## Code is given below
* **Code to find number of gravity planets**
````
gravity_planet_count = 0
for key, value in final_dict.items():
if "gravity" in value:
 gravity_planet_count += 1
print(gravity_planet_count)
````
* **Code to mfind number of planets suitable according to planet type**
````
type_planet_count = 0
for key, value in final_dict.items():
if "planet_type" in value:
 type_planet_count += 1
print(type_planet_count)
````
* **Code to find number of planets suitable according to planet type**
````
planet_not_gravity_support = []
for planet_data in planet_data_rows:
if planet_data not in low_gravity_planets:
 planet_not_gravity_support.append(planet_data)
type_no_gravity_planet_count = 0
for planet_data in planet_not_gravity_support:
if planet_data[6].lower() == "terrestrial" or planet_data[6].lower() == "super earth":
 type_no_gravity_planet_count += 1
print(type_no_gravity_planet_count)
print(type_planet_count - type_no_gravity_planet_count)
````
* **Code to find number of goldilock planets**
 ````
  if float(planet_data[8].split(" ")[0]) > 0.38 and
float(planet_data[8].split(" ")[0]) < 2:
 features_list.append("goldilock")
````
* **Code to final speed supporting planets**
````
distance = 2 * 3.14 * (float(planet_data[8].split(" ")[0]) * 1.496e+9)
 time, unit = planet_data[9].split(" ")[0], planet_data[9].split("")[1]
 if unit.lower() == "days":
 time = float(time)
 else:
 time = float(time) * 365
 time = time * 86400
 speed = distance / time
````

## Facts :
* *Now that we have the final list of habitable planets, are they really habitable? Some facts:*
   * *In our solar system, we know that the first 4 planets (Mercury, Venus, Earth and Mars) are Terrestrial Planets.*
   * *Rest of the planets are either Gas Giants or Neptune Like.*
* *The first thing we filtered out is Gravity :*
   * *Mercury - 3.7m/s*
   * *Venus - 8.87m/s*
   * *Earth - 9.8m/s*
   * *Mars - 3.8m/s*
* *We know that all these planets are Terrestrial already. Now, check the distance of these planets from the Sun.*
   * *Mercury - 0.4AU*
   * *Venus - 0.7AU*
   * *Earth - 1AU*
   * *Mars - 1.5AU.*
* *This again, makes all the planets lie in the Goldilock Zone. If we talk about the speed of these planets:*
   * *Mercury - 47km/s*
   * *Venus - 35km/s*
   * *Earth - 30km/s*
   * *Mars - 24km/s*
* *All these planets have suitable speed. Despite all the planets being clearing our filters, we are still only considering the possibility of colonizing Mars! The reason why other planets are not suitable for colonizing them:*
   * *Mercury - Mercury is not habitable since it does not have an atmosphere and its temperature varies from 100 Degree Celsius to 700 Degree Celsius.*
   * *Venus - Venus is an extreme planet. It’s very hot. It’s atmosphere traps the heat on the surface and it’s temperature is a whooping 700 Degree Celsius.It also rains sulphuric acid.*
   * *Earth - Seems like just the right planet to exist.*
   * *Mars - Mars has some atmosphere and it also has some water on its surface. The temperatures are a bit extreme (20 Degree Celsius to -150 Degree Celsius) but it’s still manageable.*
* *Apart from this, the planets could also be tidally locked to their sun. This means that one side always faces the sun and the other side always faces away from the sun.Here on Earth, we have our days warmer as compared to nights.When planets are tidally locked, one side of the planet might be extremely hot and the other side might be extremely cold.For reference, our Moon is tidally locked to our planet Earth. We can always see only one side of the moon and the other side is never visible to us.*
