# WeekendWanderer

This Python script ranks weekend places to travel based on the city provided.

## Prerequisites

Before running the script, ensure you have the following dependencies installed:
- [pandas](https://pypi.org/project/pandas/): For data manipulation and analysis.
- [pyarrow](https://pypi.org/project/pyarrow/): Required by pandas to read and write Parquet files.
- [fsspec](https://pypi.org/project/fsspec/): A Pythonic file-system abstraction layer.

You can install these dependencies using pip:

```
pip install pandas pyarrow fsspec
```

## Usage

1. Import the required libraries:
   ```python
   import pandas as pd
   ```

2. Read the travel data from the CSV file:
   ```python
   travel_data = pd.read_csv("path/to/places.csv")
   ```

3. Define the function to rank weekend places based on the city name:
   ```python
   def rank_weekend_places(city_name):
       # Filter data based on the given city
       city_data = travel_data[travel_data['City'] == city_name]
       
       # Sort places based on Google review rating
       sorted_places = city_data.sort_values(by='Google review rating', ascending=False).reset_index(drop=True)
       
       # Add serial numbers starting from 1 and rename the column to 'Rank'
       sorted_places.insert(0, 'Rank', range(1, 1 + len(sorted_places)))
       
       return sorted_places[['Rank', 'Name', 'Google review rating']]
   ```

4. Run the script and input the city name when prompted:
   ```python
   if __name__ == "__main__":
       # Input city name
       city = input("Enter the city name: ")
       
       # Rank weekend places for the given city
       ranked_places = rank_weekend_places(city)
       
       print(f"\nRanked Weekend Places to Travel in {city}:\n")
       print(ranked_places.to_string(index=False))
   ```

## Example

Suppose you have a CSV file `places.csv` containing information about various places to visit, including the city name and Google review ratings. You can use this script to rank weekend places for a specific city.

## Contributing

Contributions are welcome! If you have any suggestions or improvements, feel free to open an issue or submit a pull request.
Feel free to adjust the paths and details according to your specific use case and preferences.

