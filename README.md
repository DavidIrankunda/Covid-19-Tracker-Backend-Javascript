# Covid-19-Tracker-Backend

## Backend

The Backend is developed using Express JS

[db.js](https://github.com/dennisnderitu254/Covid-19-Tracker-Backend-/blob/main/db.js)

This File has `methods` , that establish connectivity to the `mysql` database

`Function that adds a new region to the Region table`

```
function addRegion(name) {
  const query = `
    INSERT INTO Region (Name)
    VALUES (?)
  `;

  const values = [name];

  connection.query(query, values, (err, result) => {
    if (err) {
      console.error('Error inserting region:', err);
      return;
    }
    console.log('Region inserted successfully. RegionID:', result.insertId);
  });
}
```

`Example: Add a new region`

```
addRegion('UK');
addRegion('Scotland');
addRegion('America');
addRegion('Norway');
addRegion('Sweden');
```

`Function to add a new country to the Country table`

```
function addCountry(name, isoCode, population, subregion, regionID) {
  const query = `
    INSERT INTO Country (Name, ISOCode, Population, Subregion, RegionID)
    VALUES (?, ?, ?, ?, ?)
  `;

  const values = [name, isoCode, population, subregion, regionID];

  connection.query(query, values, (err, result) => {
    if (err) {
      console.error('Error inserting country:', err);
      return;
    }
    console.log('Country inserted successfully. CountryID:', result.insertId);
  });
}
```

`Example: Add a new country`

```
addCountry('United States', 'US', 331002651, 'North America', 1);
addCountry('United Kingdom', 'GB', 67886011, 'Europe', 2);
addCountry('India', 'IN', 1380004385, 'Asia', 3);
```

`Function to add a new user to the User table`
```
function addUser(username, passwordHash, email, role, countryID) {
    const query = `
      INSERT INTO User (Username, PasswordHash, Email, Role, CountryID)
      VALUES (?, ?, ?, ?, ?)
    `;

    const values = [username, passwordHash, email, role, countryID];

    connection.query(query, values, (err, result) => {
      if (err) {
        console.error('Error inserting user:', err);
        return;
      }
      console.log('User inserted successfully. UserID:', result.insertId);
    });
  }
```

`Example: Add a new user`

```
addUser('john_doe', 'hashed_password', 'john@example.com', 'user', 1);
```

`Function to add new COVID-19 data to the COVID19Data table`
```
function addCovid19Data(countryID, date, confirmedCases, recoveredCases, fatalities) {
  const query = `
    INSERT INTO COVID19Data (CountryID, Date, ConfirmedCases, RecoveredCases, Fatalities)
    VALUES (?, ?, ?, ?, ?)
  `;

  const values = [countryID, date, confirmedCases, recoveredCases, fatalities];

  connection.query(query, values, (err, result) => {
    if (err) {
      console.error('Error inserting COVID-19 data:', err);
      return;
    }
    console.log('COVID-19 data inserted successfully. DataID:', result.insertId);
  });
}
```


`Example: Add COVID-19 data`
```
addCovid19Data(1, '2024-01-01', 1000, 500, 10);
addCovid19Data(2, '2024-01-01', 500, 200, 5);
addCovid19Data(3, '2024-01-01', 2000, 1500, 30);
```
