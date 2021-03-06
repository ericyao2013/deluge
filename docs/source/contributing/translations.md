# Translation contributions

## Translators

For translators we have a [Launchpad translations] account where you can
translate the `.po` files.

## Marking text for translation

To mark text for translation in Python and ExtJS wrap the string with the
function `_()` like this:

    torrent.set_tracker_status(_("Announce OK"))

For GTK the text can also be marked translatable in the `glade/*.ui` files:

    <property name="label" translatable="yes">Max Upload Speed:</property>

For more details see: [Python Gettext]

## Translation process

These are the overall stages in gettext translation:

`Portable Object Template -> Portable Object -> Machine Object`

- The `deluge.pot` is created using `generate_pot.py`.
- Upload `deluge/i18n/deluge.pot` to [Launchpad translations].
- Give the translators time to translate the text.
- Download the updated `.po` files from translation site.
- Extract to `deluge/i18n/` and strip the `deluge-` prefix:

       rename -f 's/^deluge-//' deluge-*.po

- The binary `MO` files for each language are generated by `setup.py`
  using the `msgfmt.py` script.

To enable Web UI to use translations update `gettext.js` by running `gen_gettext.py` script.

## Useful applications

- [podiff](http://puszcza.gnu.org.ua/projects/podiff/) - Compare textual information in two PO files
- [gtranslator](http://projects.gnome.org/gtranslator/) - GUI PO file editor
- [Poedit](http://www.poedit.net/) - GUI PO file editor

## Testing translation

Testing that translations are working correctly can be performed by running
Deluge as follows.

Create an `MO` for a single language in the correct sub-directory:

    mkdir -p deluge/i18n/fr/LC_MESSAGES
    python msgfmt.py -o deluge/i18n/fr/LC_MESSAGES/deluge.mo deluge/i18n/fr.po

Run Deluge using an alternative language:

    LANGUAGE=fr deluge
    LANGUAGE=ru_RU.UTF-8 deluge

Note: If you do not have a particular language installed on your system it
will only translate based on the `MO` files for Deluge so some GTK
text/button strings will remain in English.

[launchpad translations]: https://translations.launchpad.net/deluge/
[python gettext]: http://docs.python.org/library/gettext.html
