# TYPO3 Extension `solr`

This extension enables the extension [numbered_pagination](https://github.com/georgringer/numbered_pagination/) for EXT:solr

## Fork notes

This is webconsulting's fork of [studiomitte/solr_numbered_pagination](https://github.com/studiomitte/solr_numbered_pagination).
The Composer package name stays `studiomitte/solr-numbered-pagination`. Upstream `main` supports TYPO3 14 and EXT:solr
14, but no upstream release does yet: the newest tag, 1.0.4, stops at TYPO3 13.4. Branch `main` of this fork is
upstream `main` plus:

- **A defensive event listener.** `BeforeSearchResultIsShownEventListener` only reads `getMaxPageNumbers()` when the
  event still carries EXT:solr's `ResultsPagination`. If another listener has already replaced it, the listener
  falls back to 10 links instead of calling an undefined method. It is also `final` and builds its objects with
  `new`.
- **A Fluid partial for the numbered pagination.** `Resources/Private/Partials/Result/Pagination.html` is styled with
  shadcn/ui utility classes and has accessible labels in `Resources/Private/Language/` (English and German). It is
  not active by default; a site opts in through its EXT:solr view settings:

  ```yaml
  plugin:
    tx_solr:
      view:
        partialRootPath: 'EXT:solr_numbered_pagination/Resources/Private/Partials/'
  ```
- A TYPO3 14 style extension icon.

Installing the fork:

```json
{
    "repositories": [{"type": "vcs", "url": "https://github.com/dirnbauer/solr_numbered_pagination.git"}],
    "require": {"studiomitte/solr-numbered-pagination": "dev-main"}
}
```

The fork has no release tags, so require the branch; `composer.lock` pins the exact commit. A branch constraint
cannot resolve to an upstream tag. The `upstream` remote is fetched with `--no-tags`, and upstream changes are merged,
never rebased.

## Usage

1) Install extension with `composer require studiomitte/solr-numbered-pagination`
2) Done

## Thanks to

This extension has been developed by [Studio Mitte](https://studiomitte.com), TYPO3 agency in Linz, Austria.


## Credits

This extension was created by Georg Ringer for [Studio Mitte, Linz](https://studiomitte.com).

[Find more TYPO3 extensions we have developed](https://www.studiomitte.com/loesungen/typo3) that provide additional features for TYPO3 sites. 
