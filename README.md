# WordleMaker

This is a clone project of the popular word guessing game we all know and love. Made using React, Typescript, and Tailwind.

[**Try out the demo!**](https://wordlemaker.vercel.app/)

## Make your own

### Using Vercel (Click the button):

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fjustkorudev%2Fwordlemaker&demo-title=WordleMaker%20Demo&demo-description=Official%20WordleMaker%20Demo%20Website&demo-url=https%3A%2F%2Fworldlemaker.vercel.app%2F&demo-image=https%3A%2F%2Fi.ibb.co%2FNypXCdF%2F20301-E44-00-F1-4-F8-C-A53-F-ECA5-A429-E84-D.jpg)

### Using npm to build a dev version at a VPS:

Clone the repository and perform the following command line actions:

```bash
$> git clone https://github.com/justkorudev/wordlemaker
$> cd wordlemaker
$> npm install
$> npm run start
```

## FAQ

### How can I change the length of a guess?

The default configuration is for solutions and guesses of length five, but it is flexible enough to handle other lengths, even variable lengths each day.

To configure for a different constant length:

- Update the `WORDS` array in [src/constants/wordlist.ts](src/constants/wordlist.ts) to only include words of the new length.
- Update the `VALID_GUESSES` array in [src/constants/validGuesses.ts](src/constants/validGuesses.ts) to only include words of the new length.

To configure for variable lengths:

- Update the `WORDS` array in [src/constants/wordlist.ts](src/constants/wordlist.ts) to include words of any of the variable lengths desired.
- Update the `VALID_GUESSES` array in [src/constants/validGuesses.ts](src/constants/validGuesses.ts) to include words of any of the variable lengths desired.

Note that guesses are validated against both the length of the solution, and presence in VALID_GUESSES.

### How can I create a version in another language?

- In [.env](.env):
  - Update the title and the description
  - Set the `REACT_APP_LOCALE_STRING` to your locale
- In [public/index.html](public/index.html):
  - Update the "You need to enable JavaScript" message
  - Update the language attribute in the HTML tag
  - If the language is written right-to-left, add `dir="rtl"` to the HTML tag
- Update the name and short name in [public/manifest.json](public/manifest.json)
- Update the strings in [src/constants/strings.ts](src/constants/strings.ts)
- Add all of the five letter words in the language to [src/constants/validGuesses.ts](src/constants/validGuesses.ts), replacing the English words
- Add a list of goal words in the language to [src/constants/wordlist.ts](src/constants/wordlist.ts), replacing the English words
- Update the "Settings" modal in [src/components/modals/SettingsModal.tsx](src/components/modals/SettingsModal.tsx)
- Update the "Info" modal in [src/components/modals/InfoModal.tsx](src/components/modals/InfoModal.tsx)
- Update the "DatePicker" modal in [src/components/modals/DatePickerModal.tsx](src/components/modals/DatePickerModal.tsx)
- Update the statistics migration components modal in:
  - [src/components/stats/MigrationIntro.tsx](src/components/stats/MigrationIntro.tsx)
  - [src/components/stats/EmigratePanel.tsx](src/components/stats/EmigratePanel.tsx)
  - [src/components/stats/ImmigratePanel.tsx](src/components/stats/ImmigratePanel.tsx)
  - [src/components/modals/MigrateStatsModal.tsx](src/components/modals/MigrateStatsModal.tsx)
- To ensure that migration codes are unique to your application, update the Blowfish encryption key and initialization vector with random 30 character and 8 character strings in [src/constants/settings.ts](src/constants/settings.ts)
- If the language has letters that are not present in English update the keyboard in [src/components/keyboard/Keyboard.tsx](src/components/keyboard/Keyboard.tsx)
- If the language is written right-to-left, prepend `\u202E` (the unicode right-to-left override character) to the return statement of the inner function in `generateEmojiGrid` in
  [src/lib/share.ts](src/lib/share.ts)
- To enable replaying past days' games, set `ENABLE_ARCHIVED_GAMES` to `true`
- Set `DATE_LOCALE` to a suitable locale string as defined in [date-fns](https://github.com/date-fns/date-fns/tree/main/src/locale).

### How can I add usage tracking?

This repository includes support for Google Analytics or [Plausible Analytics](https://plausible.io), but, by default, this is disabled.

To enable Google Analytics:

- Create a Google Analytics 4 property and obtain the measurement ID (of the format `G-XXXXXXXXXX`)
- In [.env](.env), add `REACT_APP_GOOGLE_MEASUREMENT_ID=G-XXXXXXXXXX`

Keep in mind that your region might have legislation about obtaining a user's consent before enabling trackers. This is up to downstream repos to implement.

To enable Plausible Analytics:

- Create a new website with Plausible Analytics with a given domain, e.g. `example.app`
- In [.env](.env), add `REACT_APP_PLAUSIBLE_DOMAIN=example.app`

### Why does sharing of results not work?

For mobile and wearable devices and smart TVs, sharing of results is initially attempted using the [Web Share API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Share_API). For other devices or when sharing to the Web Share API fails, the results are written to the clipboard. Both these methods will succeed only in a [secure context](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts), which require you to implement the HTTPS protocol when hosting this repo on a public domain.
