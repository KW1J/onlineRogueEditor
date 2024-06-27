# V0.4

## Naming Convention
- Everything camelCase with prefixes
- Functions are prefixed with f_
- Menu Fuctions are prefixed with m_
- Enum/Data Functions will be prefixed with d_
- Fuction Helpers are prefixed with fh_
- "" for JSON and for header related stuff to make escaping easier, otherwise ''

## Bugfixes
- Fixed maxStacks in itemLogic
  - Berry Pouch from `(1)` to `(3)`
  - Vitamin Stacks from `(20)` to `(31)`
  - Hidden Ability Charm from `(3)` to `(4)`

## Additions
- Added Autocompleter Bidirectional functionality
  - You can now type either ID or Name's
- Added Autocompleter to `f_editBiomes()`, `f_addCandies()`, `f_editAccountStats()`
- Added decoration-handlers `@handle_operation_exceptions` & `@handle_error_response`
  - They are also set up for utilizing them to filter stuff.
    - ```if editOffline: term = [entry for entry in term if entry[1] != rogue.f_updateAll]```
    - This Line would in runtime filter a entry that points to f_updateAll(). Handled by the decorator.
    - Centralized response handling, if correct setup we can even do raise OperationSuccessfull('Pokeballs added.')
      - Which would lead to a colored response, that mentions the function, possibily more, and add the customMessgae on to it.
- `f_addEggsGenerator`() full rewritten;
  - New save structure from game, we now use the first egg we find as sample and if we don't find one we provided a basic that testedly works
    - Added `isShiny` and `overrideHiddenAbility` flags
    - Fixed calculation errors that were only valid ID's due to a bug, now they are all correct
    - Added sourcecode and more hints to whats going on for later repurpose
- Added function helpers
  - `fh_getIntInput()`, `fh_getChoiceInput()`, `fh_getCompleterInput()`
    - Sanitizes input, allows to escape from submenus more consistently
    - Allows easier creation of completer-inputs and such.
- When editing acc stats;
  - Removed playtime due to a recent change
  - Added 2 more options; randomize all - manual type all - manual choose one
    - Added functionality to save just some, exit out of loops with saving just some etc
- Added 4th "login" option which is just edit locally existing json without server connection (for Offline)
- Added all data as enums and generated to jsons so user can modify data
- Added specific calculated formIDs rather than setting MaxBigInt

## Rewrites
- Added functionality and decorators to handle error responses centralized
- Renamed  variable and function to comply with naming convention
- Rewritten input to use functionHelpers(`fh_`-definitions) to remove redundant code
- Rewritten save logic to key by key, allowing skip out of functions aswell just changing partials
- Added (0: Cancel) everywhere aswell as you can type `cancel`, `exit` or press `STRG+C` to escape from subMenus
  - Menus that present multiple options before saving will allow to type 0 to cancel+save;
  - or type exit / cancel to Abort without saves
  - All rewrites affect mentioned above affect those functions so far:
    - `f_editAccountStats(retested:works)` <Can now either random all, set one by choice (With AutoComplete by ID or Name) or loop over all one by one>
    - `f_editPokeballs(tested:works)` <Can now skip pokes, edit single ones or all> <Can now also skip choices>
    - `f_editTickets(tested:works)` <Works now same as pokeballs>
    - `f_restoreBackup(tested:works)` <Can now restore slot backups aswell>
    - `f_editMoney(tested:works)` <Adjusted to new input handlers>
    - `f_editHatchWaves(tested:works)` <Adjusted to new input handlers>
    - `f_changeSaveSlot(tested:works)` <Can now change Slots directly>
    - `f_submenuEditor(tested:works)` - <Can now use Autocomplete and 0Cancel>
    - `f_editBiome(tested:works)` <Can now type ID or Biome for autocomplete = case-insensitive, with autocompleter>
    - `f_addEggsGenerator(tested:works)` <Rewritten, fixed ID, better input logic>
    - `f_addCandies(tested:works)` <>
    - `f_editVouchers(tested:works)` <Can now either add single ones with autocomplete with ID/Name = case-insensitive, multiple in a loop or all at once.>
    - `f_editAchivements(tested:works)` <Can now either add single ones with autocomplete with ID/Name = case-insensitive, multiple in a loop or all at once.>
    - `f_editGamemodes(tested:works)` <Can now either add single ones with autocomplete with ID/Name = case-insensitive, multiple in a loop or all at once.>
    - `f_editPokemonParty(tested:works)`  <Now can see stats and everything, prompted as other loops>
    - `f_unlockStarters(tested:works)` <Now assigning perfect calculated IDs for all forms>
    - `f_editStarters(tested:works)`  <Same as above + new input logic>
    - `f_createBackup(tested:works)` <now creates backups for slots aswell>
    - `f_restoreBackup(tested:works)` <Should automatically recognize slot backups too>

    - Simplified:
      - `f_updateAllToServer(wip)`
      - `get_trainer_data(wip)`
      - `getSlotData(wip)`
      - `f_logout()`
      ^ Postponed.


# Removed
- print_pokedex(), print_printBiomes(), print_moves(), print_natures(), print_vouchers(), print_natureSlot()
  - replaced with fh_printEnum(type)

# And countless small bugfixes..