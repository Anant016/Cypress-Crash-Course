1. npm i cypress (--save-dev)

   > create cypress folder & install cypress GUI

2. npx cypress open /npx cypress run/ text npm run test/ npm test

3. Run all spec files in a folder -
   `npx cypress run --spec "cypress/integrations/\*\*/\*" `
4. Run single file
   `npx cypress run --spec "cypress/integrations/action.spec.js `"

### What's NPX ?

Without NPX - `node ./node_modules/.bin/mocha`

<hr/>

1. Fixtures
2. Integration
3. Plugins
4. Support - (is loaded automatically the first time)

<hr/>

Either put

` /// <reference types="cypress" />`
for every file in _integration_ folder (\*.spec.js)

or

(in root folder i.e)outside cypress folder

Have a file
`jsconfig.json`

with

```{
    "include": [
      "./node_modules/cypress",
      "cypress/**/*.js"
    ]
  }
```

<hr/>

`cypress.json` fields -

```
{
    "baseUrl" : "https://react-redux.realworld.io",
    "reporter": "cypress-multi-reporters",
    "reporterOptions": {
        "reporterEnabled": "mochawesome",
        "mochawesomeReporterOptions": {
            "reportDir": "cypress/reports/mocha",
            "quite": true,
            "overwrite": false,
            "html": false,
            "json": true
        }
    }
}
```

<hr/>

Refer - https://github.com/bushralam/Cypress

<hr/>

# Mocha Hooks

- Before
- After
- Before Each
- After Each

# TO skip a Test

Use - `only`
Hooks always run

## MochaAwesome Report Generator

npm i -D mocha cypress-multi-reporters mochaawesome mochaawesome-merge mochaawesome-report-generator

"scripts": {
"clean:reports": "rm -R -f cypress/reports && mkdir cypress/reports && mkdir cypress/reports/mochareports",
"pretest": "npm run clean:reports",
"scripts": "cypress run",
"combine-reports": "mochawesome-merge cypress/reports/mocha/\*.json > cypress/reports/mochareports/report.json",
"generate-report": "marge cypress/reports/mochareports/report.json -f report -o cypress/reports/mochareports",
"posttest": "npm run combine-reports && npm run generate-report",
"test": "npm run scripts || npm run posttest"
},

`npm run test`

# Cucumber

npm i -D cypress-cucumber-preprocessor

1. package.json
   "cypress-cucumber-preprocessor": {
   "nonGlobalStepDefinitions": true
   }

2. plugins-> index.js
   const cucumber = require('cypress-cucumber-preprocessor').default

module.exports = (on, config) => {
on('file:preprocessor', cucumber())
}

3. cypress.json
   "testFiles":"\*\*\\\*.feature"

   ````
   Feature: Login
   I want to log into Conduit
   @smoke
   Scenario: Conduit Login
   Given I open Conduit login page
   When I type in
   | username | password |
   | qamilestone.academy@gmail.com | admin123 |
   And I click on Sign in button
   Then "Your Feed" should be shown
    ```


    Tags: @smoke @focus
   ````
