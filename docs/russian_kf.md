!> In case of a fuckup you can wipe your int's and restore them from "..\Your KF Dir\System\": [GUI2K4.int](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/GUI2K4.int), [XInterface.int](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/XInterface.int) and [KFMod.int](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/KFMod.int).

- Строка ввода чата в лобби и в разных меню (map voting, kick voting, etc.):
    `GUI2K4.int` > группа `fntUT2k4Menu` (у меня 4-ый элемент - 14-ый шрифт)
- История чата в разных меню (map voting, kick voting, etc.):
    `GUI2K4.int` > группа `fntUT2k4ServerList`
- Консоль:
    `XInterface.int` > группа `HudBase`, массив `FontArrayNames` (у меня индекс 6 - 12-ый шрифт)
- Внутриигровая строка набора чата и всплывающие сообщения:
    `KFMod.int` > группа `HUDKillingFloor`, массив `FontArrayNames` (у меня индекс 6 - 12-ый шрифт)

То, что в скобках, может зависеть от выставленного размера gui, разрешения и прочего. А может и не зависеть.
Думаю нормально будет заменить все элементы массива, а не только определенные.

```js
ROFonts.ROBtsrmVr > ROFonts_RUS.ROArial
ROFontsTwo.ROArial24DS > ROFonts_Rus.ROArial24
```
