# sails-hook-sequelize-blueprints

a fork of [cesardeazevedo/sails-hook-sequelize-blueprints](https://github.com/cesardeazevedo/sails-hook-sequelize-blueprints) Sails blueprints for sequelize ORM

Diffs:

- populate by association name
- find default (not populate all)
- to populate all you will need to send `.../?populate=all`

[![Build Status](https://travis-ci.org/Puemos/sails-hook-sequelize-blueprints.svg)](https://travis-ci.org/Puemos/sails-hook-sequelize-blueprints) [![npm version](https://badge.fury.io/js/sails-hook-sequelize-blueprints.svg)](http://badge.fury.io/js/sails-hook-sequelize-blueprints)

# Install

Install [sails-hook-sequelize](https://github.com/festo/sails-hook-sequelize) first:

```sh
$ npm install sails-hook-sequelize --save
```

Install this hook with:

```sh
$ npm install sails-hook-sequelize-blueprints-puemos --save
```

Sequelize dependencies:

```sh
$ npm install --save sequelize
$ npm install --save pg pg-hstore // in case of PostgreSQL
$ npm install --save continuation-local-storage
```

# Configuration

`.sailsrc`

``` `
"hooks": {
  "blueprints": false,
  "orm": false,
  "pubsub": false
}
```

## Blueprints

Default blueprints configurations

```javascript
module.exports.blueprints = {
  actions: true,
  index: true,
  shortcuts: true,
  rest: true,
  prefix: '',
  restPrefix: '',
  pluralize: false,
  populate: true,
  defaultLimit: 30,
  populateLimit: 30,
  autoWatch: true,
}
```

## Connections

Sequelize connection

```javascript
somePostgresqlServer: {
  user: 'postgres',
  password: '',
  database: 'sequelize',
  dialect: 'postgres',
  options: {
    dialect: 'postgres',
    host   : 'localhost',
    port   : 5432,
    logging: true
  }
}
```

## Models

Sequelize model definition `models/user.js`

```javascript
module.exports = {
  attributes: {
    name: {
      type: Sequelize.STRING,
      allowNull: false
    },
    age: {
      type: Sequelize.INTEGER
    }
  },
  associations: function() {
    user.hasMany(image, {
      foreignKey: {
        name: 'owner',
        allowNull: false
      }
    });
    user.belongsToMany(affiliation, {
      as: 'affiliations',
      to: 'users', // must be named as the alias in the related Model
      through: 'UserAffiliation',
      foreignKey: {
        name: 'userId',
        as: 'affiliations'
      }
    });
  },
  options: {
    tableName: 'user',
    classMethods: {},
    instanceMethods: {},
    hooks: {}
  }
};
```

# Credits
### Sails blueprints for sequelize ORM
 [cesardeazevedo/sails-hook-sequelize-blueprints](https://github.com/cesardeazevedo/sails-hook-sequelize-blueprints)

# Contributions

1. Fork it!
2. Create your feature branch: git checkout -b my-new-feature
3. Commit your changes: git commit -m 'Add some feature'
4. Push to the branch: git push origin my-new-feature
5. Submit a pull request

# License

[MIT](./LICENSE)
