---
title: 'Language change in Angular'
metaTitle: 'Language change in Angular - Guide - Handsontable Documentation'
permalink: /next/angular-language-change-example
canonicalUrl: /angular-language-change-example
---

# Language change in Angular

[[toc]]

## Overview

The following example is an implementation of the `@handsontable/angular` component with an option to change the Context Menu language.

Select a language from the selector above the table and open the Context Menu to see the result.

## Example

::: example :angular-languages --html 1 --js 2
```html
<app-root></app-root>
```
```js
// app.component.ts
import { Component } from '@angular/core';
import { getLanguagesDictionaries } from 'handsontable/i18n';
import { createSpreadsheetData } from './helpers';

@Component({
  selector: 'app-root',
  template: `
  <div class="controls"><label>Select language:
  <select [(ngModel)]="language">
    <option *ngFor="let l of languages" [value]="l.languageCode">{{l.languageCode}}</option>
  </select></label></div>
  <div>
    <hot-table [language]="language" [settings]="hotSettings"></hot-table>
  </div>
  `,
})
class AppComponent {
  hotSettings: Handsontable.GridSettings = {
    data: createSpreadsheetData(5, 10),
    colHeaders: true,
    rowHeaders: true,
    contextMenu: true,
    height: 'auto',
    licenseKey: 'non-commercial-and-evaluation'
  };
  language = 'en-US';
  languages = getLanguagesDictionaries();
}

// app.module.ts
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { BrowserModule } from '@angular/platform-browser';
import { HotTableModule } from '@handsontable/angular';
import { registerAllModules } from 'handsontable/registry';

// register Handsontable's modules
registerAllModules();

@NgModule({
  imports:      [ BrowserModule, FormsModule, HotTableModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
class AppModule { }

// bootstrap
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

platformBrowserDynamic().bootstrapModule(AppModule).catch(err => { console.error(err) });
```

## Related articles

### Related guides

- [Language](@/guides/internationalization/language.md)
- [Layout direction](@/guides/internationalization/layout-direction.md)
- [Locale](@/guides/internationalization/locale.md)

### Related API reference

- Configuration options:
  - [`language`](@/api/options.md#language)
  - [`layoutDirection`](@/api/options.md#layoutdirection)
  - [`locale`](@/api/options.md#locale)
- Core methods:
  - [`getDirectionFactor()`](@/api/core.md#getdirectionfactor)
  - [`getTranslatedPhrase()`](@/api/core.md#gettranslatedphrase)
  - [`isLtr()`](@/api/core.md#isltr)
  - [`isRtl()`](@/api/core.md#isrtl)
- Hooks:
  - [`afterLanguageChange`](@/api/hooks.md#afterlanguagechange)
  - [`beforeLanguageChange`](@/api/hooks.md#beforelanguagechange)