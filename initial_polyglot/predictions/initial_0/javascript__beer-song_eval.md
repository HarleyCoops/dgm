+ set -e
+ '[' '!' -e node_modules ']'
+ ln -s /npm-install/node_modules .
+ '[' '!' -e package-lock.json ']'
+ ln -s /npm-install/package-lock.json .
+ sed -i 's/\bxtest(/test(/g' beer-song.spec.js
+ npm run test

> test
> jest ./*

FAIL ./beer-song.spec.js
  Beer Song
    verse
      single verse
        ✕ first generic verse (12 ms)
        ✕ last generic verse (1 ms)
        ✕ verse with 2 bottles
        ✕ verse with 1 bottle (1 ms)
        ✕ verse with 0 bottles (1 ms)
    lyrics
      multiple verses
        ✕ first two verses (1 ms)
        ✕ last three verses (1 ms)
        ✕ all verses (1 ms)

  ● Beer Song › verse › single verse › first generic verse

    expect(received).toEqual(expected) // deep equality

    Expected: ["99 bottles of beer on the wall, 99 bottles of beer.", "Take one down and pass it around, 98 bottles of beer on the wall."]
    Received: "99 bottles of beer on the wall, 99 bottles of beer.
    Take one down and pass it around, 98 bottles of beer on the wall."

       5 |     describe('single verse', () => {
       6 |       test('first generic verse', () => {
    >  7 |         expect(recite(99, 1)).toEqual([
         |                               ^
       8 |           '99 bottles of beer on the wall, 99 bottles of beer.',
       9 |           'Take one down and pass it around, 98 bottles of beer on the wall.',
      10 |         ]);

      at Object.toEqual (beer-song.spec.js:7:31)

  ● Beer Song › verse › single verse › last generic verse

    expect(received).toEqual(expected) // deep equality

    Expected: ["3 bottles of beer on the wall, 3 bottles of beer.", "Take one down and pass it around, 2 bottles of beer on the wall."]
    Received: "3 bottles of beer on the wall, 3 bottles of beer.
    Take one down and pass it around, 2 bottles of beer on the wall."

      12 |
      13 |       test('last generic verse', () => {
    > 14 |         expect(recite(3, 1)).toEqual([
         |                              ^
      15 |           '3 bottles of beer on the wall, 3 bottles of beer.',
      16 |           'Take one down and pass it around, 2 bottles of beer on the wall.',
      17 |         ]);

      at Object.toEqual (beer-song.spec.js:14:30)

  ● Beer Song › verse › single verse › verse with 2 bottles

    expect(received).toEqual(expected) // deep equality

    Expected: ["2 bottles of beer on the wall, 2 bottles of beer.", "Take one down and pass it around, 1 bottle of beer on the wall."]
    Received: "2 bottles of beer on the wall, 2 bottles of beer.
    Take one down and pass it around, 1 bottle of beer on the wall."

      19 |
      20 |       test('verse with 2 bottles', () => {
    > 21 |         expect(recite(2, 1)).toEqual([
         |                              ^
      22 |           '2 bottles of beer on the wall, 2 bottles of beer.',
      23 |           'Take one down and pass it around, 1 bottle of beer on the wall.',
      24 |         ]);

      at Object.toEqual (beer-song.spec.js:21:30)

  ● Beer Song › verse › single verse › verse with 1 bottle

    expect(received).toEqual(expected) // deep equality

    Expected: ["1 bottle of beer on the wall, 1 bottle of beer.", "Take it down and pass it around, no more bottles of beer on the wall."]
    Received: "1 bottle of beer on the wall, 1 bottle of beer.
    Take it down and pass it around, no more bottles of beer on the wall.·
    No more bottles of beer on the wall, no more bottles of beer.
    Go to the store and buy some more, 99 bottles of beer on the wall."

      26 |
      27 |       test('verse with 1 bottle', () => {
    > 28 |         expect(recite(1, 1)).toEqual([
         |                              ^
      29 |           '1 bottle of beer on the wall, 1 bottle of beer.',
      30 |           'Take it down and pass it around, no more bottles of beer on the wall.',
      31 |         ]);

      at Object.toEqual (beer-song.spec.js:28:30)

  ● Beer Song › verse › single verse › verse with 0 bottles

    expect(received).toEqual(expected) // deep equality

    Expected: ["No more bottles of beer on the wall, no more bottles of beer.", "Go to the store and buy some more, 99 bottles of beer on the wall."]
    Received: ""

      33 |
      34 |       test('verse with 0 bottles', () => {
    > 35 |         expect(recite(0, 1)).toEqual([
         |                              ^
      36 |           'No more bottles of beer on the wall, no more bottles of beer.',
      37 |           'Go to the store and buy some more, 99 bottles of beer on the wall.',
      38 |         ]);

      at Object.toEqual (beer-song.spec.js:35:30)

  ● Beer Song › lyrics › multiple verses › first two verses

    expect(received).toEqual(expected) // deep equality

    Expected: ["99 bottles of beer on the wall, 99 bottles of beer.", "Take one down and pass it around, 98 bottles of beer on the wall.", "", "98 bottles of beer on the wall, 98 bottles of beer.", "Take one down and pass it around, 97 bottles of beer on the wall."]
    Received: "99 bottles of beer on the wall, 99 bottles of beer.
    Take one down and pass it around, 98 bottles of beer on the wall.·
    98 bottles of beer on the wall, 98 bottles of beer.
    Take one down and pass it around, 97 bottles of beer on the wall."

      44 |     describe('multiple verses', () => {
      45 |       test('first two verses', () => {
    > 46 |         expect(recite(99, 2)).toEqual([
         |                               ^
      47 |           '99 bottles of beer on the wall, 99 bottles of beer.',
      48 |           'Take one down and pass it around, 98 bottles of beer on the wall.',
      49 |           '',

      at Object.toEqual (beer-song.spec.js:46:31)

  ● Beer Song › lyrics › multiple verses › last three verses

    expect(received).toEqual(expected) // deep equality

    Expected: ["2 bottles of beer on the wall, 2 bottles of beer.", "Take one down and pass it around, 1 bottle of beer on the wall.", "", "1 bottle of beer on the wall, 1 bottle of beer.", "Take it down and pass it around, no more bottles of beer on the wall.", "", "No more bottles of beer on the wall, no more bottles of beer.", "Go to the store and buy some more, 99 bottles of beer on the wall."]
    Received: "2 bottles of beer on the wall, 2 bottles of beer.
    Take one down and pass it around, 1 bottle of beer on the wall.·
    1 bottle of beer on the wall, 1 bottle of beer.
    Take it down and pass it around, no more bottles of beer on the wall."

      54 |
      55 |       test('last three verses', () => {
    > 56 |         expect(recite(2, 3)).toEqual([
         |                              ^
      57 |           '2 bottles of beer on the wall, 2 bottles of beer.',
      58 |           'Take one down and pass it around, 1 bottle of beer on the wall.',
      59 |           '',

      at Object.toEqual (beer-song.spec.js:56:30)

  ● Beer Song › lyrics › multiple verses › all verses

    expect(received).toEqual(expected) // deep equality

    Expected: ["99 bottles of beer on the wall, 99 bottles of beer.", "Take one down and pass it around, 98 bottles of beer on the wall.", "", "98 bottles of beer on the wall, 98 bottles of beer.", "Take one down and pass it around, 97 bottles of beer on the wall.", "", "97 bottles of beer on the wall, 97 bottles of beer.", "Take one down and pass it around, 96 bottles of beer on the wall.", "", "96 bottles of beer on the wall, 96 bottles of beer.", …]
    Received: "99 bottles of beer on the wall, 99 bottles of beer.
    Take one down and pass it around, 98 bottles of beer on the wall.·
    98 bottles of beer on the wall, 98 bottles of beer.
    Take one down and pass it around, 97 bottles of beer on the wall.·
    97 bottles of beer on the wall, 97 bottles of beer.
    Take one down and pass it around, 96 bottles of beer on the wall.·
    96 bottles of beer on the wall, 96 bottles of beer.
    Take one down and pass it around, 95 bottles of beer on the wall.·
    95 bottles of beer on the wall, 95 bottles of beer.
    Take one down and pass it around, 94 bottles of beer on the wall.·
    94 bottles of beer on the wall, 94 bottles of beer.
    Take one down and pass it around, 93 bottles of beer on the wall.·
    93 bottles of beer on the wall, 93 bottles of beer.
    Take one down and pass it around, 92 bottles of beer on the wall.·
    92 bottles of beer on the wall, 92 bottles of beer.
    Take one down and pass it around, 91 bottles of beer on the wall.·
    91 bottles of beer on the wall, 91 bottles of beer.
    Take one down and pass it around, 90 bottles of beer on the wall.·
    90 bottles of beer on the wall, 90 bottles of beer.
    Take one down and pass it around, 89 bottles of beer on the wall.·
    89 bottles of beer on the wall, 89 bottles of beer.
    Take one down and pass it around, 88 bottles of beer on the wall.·
    88 bottles of beer on the wall, 88 bottles of beer.
    Take one down and pass it around, 87 bottles of beer on the wall.·
    87 bottles of beer on the wall, 87 bottles of beer.
    Take one down and pass it around, 86 bottles of beer on the wall.·
    86 bottles of beer on the wall, 86 bottles of beer.
    Take one down and pass it around, 85 bottles of beer on the wall.·
    85 bottles of beer on the wall, 85 bottles of beer.
    Take one down and pass it around, 84 bottles of beer on the wall.·
    84 bottles of beer on the wall, 84 bottles of beer.
    Take one down and pass it around, 83 bottles of beer on the wall.·
    83 bottles of beer on the wall, 83 bottles of beer.
    Take one down and pass it around, 82 bottles of beer on the wall.·
    82 bottles of beer on the wall, 82 bottles of beer.
    Take one down and pass it around, 81 bottles of beer on the wall.·
    81 bottles of beer on the wall, 81 bottles of beer.
    Take one down and pass it around, 80 bottles of beer on the wall.·
    80 bottles of beer on the wall, 80 bottles of beer.
    Take one down and pass it around, 79 bottles of beer on the wall.·
    79 bottles of beer on the wall, 79 bottles of beer.
    Take one down and pass it around, 78 bottles of beer on the wall.·
    78 bottles of beer on the wall, 78 bottles of beer.
    Take one down and pass it around, 77 bottles of beer on the wall.·
    77 bottles of beer on the wall, 77 bottles of beer.
    Take one down and pass it around, 76 bottles of beer on the wall.·
    76 bottles of beer on the wall, 76 bottles of beer.
    Take one down and pass it around, 75 bottles of beer on the wall.·
    75 bottles of beer on the wall, 75 bottles of beer.
    Take one down and pass it around, 74 bottles of beer on the wall.·
    74 bottles of beer on the wall, 74 bottles of beer.
    Take one down and pass it around, 73 bottles of beer on the wall.·
    73 bottles of beer on the wall, 73 bottles of beer.
    Take one down and pass it around, 72 bottles of beer on the wall.·
    72 bottles of beer on the wall, 72 bottles of beer.
    Take one down and pass it around, 71 bottles of beer on the wall.·
    71 bottles of beer on the wall, 71 bottles of beer.
    Take one down and pass it around, 70 bottles of beer on the wall.·
    70 bottles of beer on the wall, 70 bottles of beer.
    Take one down and pass it around, 69 bottles of beer on the wall.·
    69 bottles of beer on the wall, 69 bottles of beer.
    Take one down and pass it around, 68 bottles of beer on the wall.·
    68 bottles of beer on the wall, 68 bottles of beer.
    Take one down and pass it around, 67 bottles of beer on the wall.·
    67 bottles of beer on the wall, 67 bottles of beer.
    Take one down and pass it around, 66 bottles of beer on the wall.·
    66 bottles of beer on the wall, 66 bottles of beer.
    Take one down and pass it around, 65 bottles of beer on the wall.·
    65 bottles of beer on the wall, 65 bottles of beer.
    Take one down and pass it around, 64 bottles of beer on the wall.·
    64 bottles of beer on the wall, 64 bottles of beer.
    Take one down and pass it around, 63 bottles of beer on the wall.·
    63 bottles of beer on the wall, 63 bottles of beer.
    Take one down and pass it around, 62 bottles of beer on the wall.·
    62 bottles of beer on the wall, 62 bottles of beer.
    Take one down and pass it around, 61 bottles of beer on the wall.·
    61 bottles of beer on the wall, 61 bottles of beer.
    Take one down and pass it around, 60 bottles of beer on the wall.·
    60 bottles of beer on the wall, 60 bottles of beer.
    Take one down and pass it around, 59 bottles of beer on the wall.·
    59 bottles of beer on the wall, 59 bottles of beer.
    Take one down and pass it around, 58 bottles of beer on the wall.·
    58 bottles of beer on the wall, 58 bottles of beer.
    Take one down and pass it around, 57 bottles of beer on the wall.·
    57 bottles of beer on the wall, 57 bottles of beer.
    Take one down and pass it around, 56 bottles of beer on the wall.·
    56 bottles of beer on the wall, 56 bottles of beer.
    Take one down and pass it around, 55 bottles of beer on the wall.·
    55 bottles of beer on the wall, 55 bottles of beer.
    Take one down and pass it around, 54 bottles of beer on the wall.·
    54 bottles of beer on the wall, 54 bottles of beer.
    Take one down and pass it around, 53 bottles of beer on the wall.·
    53 bottles of beer on the wall, 53 bottles of beer.
    Take one down and pass it around, 52 bottles of beer on the wall.·
    52 bottles of beer on the wall, 52 bottles of beer.
    Take one down and pass it around, 51 bottles of beer on the wall.·
    51 bottles of beer on the wall, 51 bottles of beer.
    Take one down and pass it around, 50 bottles of beer on the wall.·
    50 bottles of beer on the wall, 50 bottles of beer.
    Take one down and pass it around, 49 bottles of beer on the wall.·
    49 bottles of beer on the wall, 49 bottles of beer.
    Take one down and pass it around, 48 bottles of beer on the wall.·
    48 bottles of beer on the wall, 48 bottles of beer.
    Take one down and pass it around, 47 bottles of beer on the wall.·
    47 bottles of beer on the wall, 47 bottles of beer.
    Take one down and pass it around, 46 bottles of beer on the wall.·
    46 bottles of beer on the wall, 46 bottles of beer.
    Take one down and pass it around, 45 bottles of beer on the wall.·
    45 bottles of beer on the wall, 45 bottles of beer.
    Take one down and pass it around, 44 bottles of beer on the wall.·
    44 bottles of beer on the wall, 44 bottles of beer.
    Take one down and pass it around, 43 bottles of beer on the wall.·
    43 bottles of beer on the wall, 43 bottles of beer.
    Take one down and pass it around, 42 bottles of beer on the wall.·
    42 bottles of beer on the wall, 42 bottles of beer.
    Take one down and pass it around, 41 bottles of beer on the wall.·
    41 bottles of beer on the wall, 41 bottles of beer.
    Take one down and pass it around, 40 bottles of beer on the wall.·
    40 bottles of beer on the wall, 40 bottles of beer.
    Take one down and pass it around, 39 bottles of beer on the wall.·
    39 bottles of beer on the wall, 39 bottles of beer.
    Take one down and pass it around, 38 bottles of beer on the wall.·
    38 bottles of beer on the wall, 38 bottles of beer.
    Take one down and pass it around, 37 bottles of beer on the wall.·
    37 bottles of beer on the wall, 37 bottles of beer.
    Take one down and pass it around, 36 bottles of beer on the wall.·
    36 bottles of beer on the wall, 36 bottles of beer.
    Take one down and pass it around, 35 bottles of beer on the wall.·
    35 bottles of beer on the wall, 35 bottles of beer.
    Take one down and pass it around, 34 bottles of beer on the wall.·
    34 bottles of beer on the wall, 34 bottles of beer.
    Take one down and pass it around, 33 bottles of beer on the wall.·
    33 bottles of beer on the wall, 33 bottles of beer.
    Take one down and pass it around, 32 bottles of beer on the wall.·
    32 bottles of beer on the wall, 32 bottles of beer.
    Take one down and pass it around, 31 bottles of beer on the wall.·
    31 bottles of beer on the wall, 31 bottles of beer.
    Take one down and pass it around, 30 bottles of beer on the wall.·
    30 bottles of beer on the wall, 30 bottles of beer.
    Take one down and pass it around, 29 bottles of beer on the wall.·
    29 bottles of beer on the wall, 29 bottles of beer.
    Take one down and pass it around, 28 bottles of beer on the wall.·
    28 bottles of beer on the wall, 28 bottles of beer.
    Take one down and pass it around, 27 bottles of beer on the wall.·
    27 bottles of beer on the wall, 27 bottles of beer.
    Take one down and pass it around, 26 bottles of beer on the wall.·
    26 bottles of beer on the wall, 26 bottles of beer.
    Take one down and pass it around, 25 bottles of beer on the wall.·
    25 bottles of beer on the wall, 25 bottles of beer.
    Take one down and pass it around, 24 bottles of beer on the wall.·
    24 bottles of beer on the wall, 24 bottles of beer.
    Take one down and pass it around, 23 bottles of beer on the wall.·
    23 bottles of beer on the wall, 23 bottles of beer.
    Take one down and pass it around, 22 bottles of beer on the wall.·
    22 bottles of beer on the wall, 22 bottles of beer.
    Take one down and pass it around, 21 bottles of beer on the wall.·
    21 bottles of beer on the wall, 21 bottles of beer.
    Take one down and pass it around, 20 bottles of beer on the wall.·
    20 bottles of beer on the wall, 20 bottles of beer.
    Take one down and pass it around, 19 bottles of beer on the wall.·
    19 bottles of beer on the wall, 19 bottles of beer.
    Take one down and pass it around, 18 bottles of beer on the wall.·
    18 bottles of beer on the wall, 18 bottles of beer.
    Take one down and pass it around, 17 bottles of beer on the wall.·
    17 bottles of beer on the wall, 17 bottles of beer.
    Take one down and pass it around, 16 bottles of beer on the wall.·
    16 bottles of beer on the wall, 16 bottles of beer.
    Take one down and pass it around, 15 bottles of beer on the wall.·
    15 bottles of beer on the wall, 15 bottles of beer.
    Take one down and pass it around, 14 bottles of beer on the wall.·
    14 bottles of beer on the wall, 14 bottles of beer.
    Take one down and pass it around, 13 bottles of beer on the wall.·
    13 bottles of beer on the wall, 13 bottles of beer.
    Take one down and pass it around, 12 bottles of beer on the wall.·
    12 bottles of beer on the wall, 12 bottles of beer.
    Take one down and pass it around, 11 bottles of beer on the wall.·
    11 bottles of beer on the wall, 11 bottles of beer.
    Take one down and pass it around, 10 bottles of beer on the wall.·
    10 bottles of beer on the wall, 10 bottles of beer.
    Take one down and pass it around, 9 bottles of beer on the wall.·
    9 bottles of beer on the wall, 9 bottles of beer.
    Take one down and pass it around, 8 bottles of beer on the wall.·
    8 bottles of beer on the wall, 8 bottles of beer.
    Take one down and pass it around, 7 bottles of beer on the wall.·
    7 bottles of beer on the wall, 7 bottles of beer.
    Take one down and pass it around, 6 bottles of beer on the wall.·
    6 bottles of beer on the wall, 6 bottles of beer.
    Take one down and pass it around, 5 bottles of beer on the wall.·
    5 bottles of beer on the wall, 5 bottles of beer.
    Take one down and pass it around, 4 bottles of beer on the wall.·
    4 bottles of beer on the wall, 4 bottles of beer.
    Take one down and pass it around, 3 bottles of beer on the wall.·
    3 bottles of beer on the wall, 3 bottles of beer.
    Take one down and pass it around, 2 bottles of beer on the wall.·
    2 bottles of beer on the wall, 2 bottles of beer.
    Take one down and pass it around, 1 bottle of beer on the wall.·
    1 bottle of beer on the wall, 1 bottle of beer.
    Take it down and pass it around, no more bottles of beer on the wall."

      67 |
      68 |       test('all verses', () => {
    > 69 |         expect(recite(99, 100)).toEqual([
         |                                 ^
      70 |           '99 bottles of beer on the wall, 99 bottles of beer.',
      71 |           'Take one down and pass it around, 98 bottles of beer on the wall.',
      72 |           '',

      at Object.toEqual (beer-song.spec.js:69:33)

Test Suites: 1 failed, 1 total
Tests:       8 failed, 8 total
Snapshots:   0 total
Time:        4.756 s
Ran all test suites matching /.\/LICENSE|.\/babel.config.js|.\/beer-song.js|.\/beer-song.spec.js|.\/eval.sh|.\/node_modules|.\/package-lock.json|.\/package.json/i.
npm notice
npm notice New major version of npm available! 10.8.2 -> 11.3.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.3.0
npm notice To update run: npm install -g npm@11.3.0
npm notice
