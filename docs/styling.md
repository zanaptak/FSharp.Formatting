---
category: Documentation
categoryindex: 1
index: 7
---
# Customization and Styling 

When using `fsdocs`, there are six levels of extra content development and styling.

1. Don't do any styling or documentation customization and simply write content.  This is by far the simplest option to maintain.

2. Add content such as an `docs/index.md` to customize the front-page content for your generated docs.
   You can also add content such as `docs/reference/fslib.md` to give a bespoke landing page
   for one of your namespaces, e.g. here assumed to be `namespace FsLib`.  This will override any
   generated content.

3. Customize via Styling Parameters

4. Customize via CSS

5. Customize via a new template

6. Customize by generating your own site using your own code

By default `fsdocs` does no styling customization and uses the following defaults. These are the settings used to build this site.

* Uses the default template in [docs/_template.html](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/_template.html)

* Uses the default styles in [docs/content/fsdocs-default.css](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/content/fsdocs-default.css).

* Uses no custom styles in [docs/content/fsdocs-custom.css](https://github.com/fsprojects/FSharp.Formatting/blob/master/docs/content/fsdocs-default.css).

* Uses no styling parameters except those extracted from the project files.

For your project, you don't need any of these files. However you can add them if you wish, though if
you adjust them there is no guarantee that your template will continue to work with future versions of F# Formatting.

## Customizing via Styling Parameters

The following [content parameters](content.html) are particularly related to visual styling:

|  Substitution name                  | Value (if not overriden by --parameters)                      | 
|:------------------------------------|:--------------------------------------------------------------|
| `fsdocs-authors`              | `<Authors>`                                                   |  
| `fsdocs-collection-name-link` | `<FsDocsCollectionNameLink>`        |  
| `fsdocs-license-link`         | `<FsDocsLicenseLink>`  | 
| `fsdocs-logo-src`             | `<FsDocsLogoSource>` |  
| `fsdocs-logo-link`            | `<FsDocsLogoLink>`   |                
| `fsdocs-navbar-position`      | `<FsDocsNavbarPosition>` (`fixed-left` or `fixed-right`)     |  
| `fsdocs-release-notes-link`   | `<FsDocsReleaseNotesLink>` else `<PackageProjectUrl>/blob/master/RELEASE_NOTES.md`  | 
| `fsdocs-repository-link`      | `<RepositoryUrl>`                                             | 
| `fsdocs-theme`                | `<FsDocsTheme>`, must currently be `default`    | 

These basic entry-level styling parameters can be set in the project file or `Directory.Build.props`.
For example:

```xml
    <!-- Example ultra-simple styling and generation settings for FsDocs default template-->
    <PackageLicenseUrl>https://github.com/foo/bar/blob/master/License.txt</PackageLicenseUrl>
    <PackageProjectUrl>https://foo.github.io/bar/</PackageProjectUrl>
    <RepositoryUrl>https://github.com/foo/bar/</RepositoryUrl>
    <FsDocsLogoLink>https://fsharp.org</FsDocsLogoLink>
    <FsDocsLicenseLink>https://github.com/foo/bar/blob/master/License.txt</FsDocsLicenseLink>
    <FsDocsReleaseNotesLink>https://github.com/foo/bar/blob/master/release-notes.md</FsDocsReleaseNotesLink>
    <FsDocsNavbarPosition>fixed-left</FsDocsNavbarPosition>
    <FsDocsWarnOnMissingDocs>true</FsDocsWarnOnMissingDocs>
    <FsDocsTheme>default</FsDocsTheme>
```

As an example, here is [a page with `fsdocs-navbar-position` set to `fixed-right`](templates/leftside/styling.html).

## Customizing via CSS

You can start styling by creating a file `docs/content/fsdocs-custom.css` and adding entries to it.  It is loaded by
the standard template.  The CSS classes of generated content are:

|  CSS class   | Corresponding Content|  
|:------------------------------------|:--------------------------------------------------------------|
| `.fsdocs-tip`              |   generated tooltips                                                  |  
| `.fsdocs-xmldoc`      |  generated xmldoc sections  |
| `.fsdocs-member-list`      |  generated member lists (tables)  |
| `.fsdocs-member-usage`      |  usage in generated member lists  |
| `.fsdocs-member-tooltip`      |  tooltips in generated member lists |
| `.fsdocs-member-xmldoc`      |  documentation in generated member lists |
| `.fsdocs-entity-list`      |  generated entity lists |
| `.fsdocs-entity-name`      |  generated entity lists |
| `.fsdocs-entity-xmldoc`      |  documentation in generated entity lists |
| `.fsdocs-exception-list`      |  generated exception lists |
| `.fsdocs-summary`      |  the 'summary' section of an XML doc |
| `.fsdocs-remarks`      |  the 'remarks' section of an XML doc |
| `.fsdocs-params`      |  the 'parameters' section of an XML doc |
| `.fsdocs-param`      |  a 'parameter' section of an XML doc |
| `.fsdocs-param-name`      |  a 'parameter' name of an XML doc |
| `.fsdocs-returns`      |  the 'returns' section of an XML doc |
| `.fsdocs-example`      |  the 'example' section of an XML doc |
| `.fsdocs-note`      |  the 'notes' section of an XML doc |
| `.fsdocs-para`      |  a paragraph of an XML doc |

Some generated elements are given specific HTML ids:

|  HTML Element Id    | Content|  
|:------------------------------------|:--------------------------------------------------------------|
| `#fsdocs-content`              |    The generated content |  
| `#fsdocs-searchbox `      |   The search box |
| `#fsdocs-logo `      |  The logo |
| `#fsdocs-nav `      |  The navigation-bar |

If you write a new theme by CSS styling please contribute it back to FSharp.Formatting.

## Customizing via a new template

You can do advanced styling by creating a new template.  Add a file `docs/_template.html`, likely starting
with the existing default template.

> NOTE: To enable hot reload during development with `fsdocs watch` in a custom `_template.html` file,
> make sure to add the single line `{{fsdocs-watch-script}}`  to your `<head>` tag.

> NOTE: There is no guarantee that your template will continue to work with future versions of F# Formatting.
> If you do develop a good template please consider contributing it back to F# Formatting.

## Customizing menu items by template

You can add advanced styling to the sidebar generated menu items by creating a new template for it.
`fsdoc` will look for menu templates in the `--input` folder which defaults to the docs folder.

To customize the generated menu-item headers, use file `_menu_template.html` with starting template:

```html
<li class="nav-header">
    {{fsdocs-menu-header-content}}
</li>
{{fsdocs-menu-items}}
```

Similarly, to customize the individual menu item list, use file `_menu-item_template.html` with starting template:

```html
<li class="nav-item"><a href="{{fsdocs-menu-item-link}}" class="nav-link">{{fsdocs-menu-item-content}}</a></li>
```
Do note that files need to be added prior running or won't be generated.
In case you want to get a unique identifier for a header or menu item, you can use `{{fsdocs-menu-header-id}}` and `{{fsdocs-menu-item-id}}`, respectively.

## Customizing by generating your own site using your own code

The `FSharp.Formatting.ApiDocs` namespace includes a `GenerateModel` that captures
the results of documentation preparation in `ApiDocsModel` and allows you to 
generate your own site using your own code.

> NOTE: The ApiDocsModel API is undergoing change and improvement and there is no guarantee that your bespoke site generation will continue to work
> with future versions of F# Formatting.

> NOTE: The `ApiDocsModel` currently includes some generated HTML with some specific style tags.
> In the long term these may be removed from the design of that component.

