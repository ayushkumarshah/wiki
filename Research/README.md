# QDGGA

Query-Driven Global Graph Attention Model for Visual Parsing: Recognizing
Handwritten and Typeset Math Formulas

## Installing requirements

```zsh
pip install -r requirements.txt
```

## Running the prediction

### Example (Infty dataset - typeset formula images): 

```python
python test.py --config config/infty.yaml
```

If you want to over-ride the default configurations,

```python
python test.py \
--config config/infty.yaml \
--data_dir data/infty/IMG \
--lg_dir data/infty/LG_test_corrected \
--use_gt 0 \
--output_dir run/ \
--img_list data/infty/small_Testing.txt \
--model_name infty_stroke_newBest
```

Using short arguments:

```python
python test.py \
-c config/infty.yaml 
-dd data/infty/IMG \
-l data/infty/LG_test \
-u 0 \
-o run/ \
-i data/infty/small_Testing.txt \
-m infty_stroke_newBest
```

### Example (CROHME dataset - handwritten formula strokes): 

```python
python test.py --config config/crohme.yaml
```

If you want to over-ride the default configurations,

```python
python test.py \
--config config/crohme.yaml \
--data_dir data/test2019 \
--use_gt 0 \
--output_dir run/ \
--model_name 3branchAtt_REL_mode2_4CH
```

Using short arguments:

```python
python test.py \
-c config/crohme.yaml
-dd data/test2019 \
-u 0 \
-o run/ \
-m 3branchAtt_REL_mode2_4CH
```

## Running the web api

### Health check

To check, whether the web service is running, goto [`northbay.cs.rit.edu:5050`](northbay.cs.rit.edu:5050)

### Running the parser

Use the endpoint [`northbay.cs.rit.edu:5050/predict`](northbay.cs.rit.edu:5050/predict)

Input JSON formats:

#### Handwritten formula strokes as input

```json
{
  "request_time": "2021-01-22T06:36:34",
  "input_type": "strokes",
  "file_id": "string",
  "annotation": "string",
  "input_strokes": [
    {
      "points": "string",
      "id": "string"
    },
    {
      "points": "string",
      "id": "string"
    },
    ...,
    {
      "points": "string",
      "id": "string"
    }
  ]
}
```

Example:

```json
{
    "request_time": "2021-01-20T11:46",
    "input_type": "strokes",
    "file_id": "ISICal19_1201_em_751",
    "annotation": "string",
    "input_strokes": [
        {
            "points": "18 105, 18 104, 18 103, 18 102, 18 101, 18 100, 19 99, 20 98, 21 97, 22 95, 24 94, 25 93, 26 93, 26 92, 27 92, 28 92, 29 92, 30 92, 31 92, 33 92, 34 92, 36 93, 37 93, 38 94, 39 95, 40 96, 41 101, 42 102, 42 104, 42 106, 42 107, 42 111, 41 113, 41 115, 40 117, 40 119, 39 121, 38 125, 37 126, 36 128, 35 130, 34 131, 33 133, 32 135, 30 138, 30 137, 31 135, 35 127, 36 124, 37 122, 39 120, 40 118, 42 116, 45 112, 46 110, 47 108, 48 107, 48 106, 49 105, 51 102, 51 101, 52 101, 51 101, 49 102, 48 103, 46 105, 45 106, 44 108, 43 110, 41 116, 41 117, 41 118, 41 119, 43 121, 45 123, 47 123, 49 124, 51 125, 54 125, 56 125, 61 125, 62 125, 63 124, 64 124, 64 123, 63 123, 62 123",
            "id": "0"
        },
        {
            "points": "77 78, 78 77, 78 76, 77 77, 76 78, 75 79, 74 80, 73 82, 72 83, 72 84, 71 86, 70 87, 69 89, 69 91, 68 92, 68 93, 68 94, 68 96, 67 97, 67 96, 67 95",
            "id": "1"
        },
        {
            "points": "88 109, 87 109, 86 109, 85 109, 84 109, 83 109, 82 109, 81 108, 82 108, 84 108, 85 107, 87 107, 89 107, 90 106, 92 106, 93 105, 96 105, 97 105, 98 104, 99 104, 100 104",
            "id": "2"
        },
        {
            "points": "84 122, 83 122, 84 122, 86 122, 88 121, 90 120, 92 120, 95 119, 100 118, 102 117, 103 117, 104 117, 103 117",
            "id": "3"
        },
        {
            "points": "150 57, 149 57, 148 57, 147 58, 146 59, 145 60, 144 62, 143 63, 142 64, 141 65, 140 67, 139 68, 138 70, 138 72, 137 75, 136 77, 136 79, 135 86, 135 88, 135 90, 135 93, 135 95, 135 100, 135 103, 135 105, 135 107, 136 109, 137 111, 139 115, 140 117, 141 119, 142 120, 144 122, 145 123, 148 125, 150 126, 152 127, 154 128, 156 128, 157 129, 158 129, 161 130, 162 130, 163 130, 163 129, 162 127",
            "id": "4"
        },
        {
            "points": "193 85, 194 84, 194 83, 194 82, 194 81, 194 80, 194 79, 193 78, 192 78, 192 77, 191 76, 190 76, 189 76, 188 75, 187 75, 186 75, 185 75, 184 75, 183 76, 181 77, 179 79, 177 81, 176 83, 174 84, 173 85, 172 87, 170 88, 167 93, 167 94, 166 95, 165 96, 165 97, 165 99, 165 100, 165 101, 165 102, 166 102, 167 103, 169 103, 173 103, 174 103, 176 102, 177 101, 179 100, 182 97, 183 96, 185 94, 186 93, 187 91, 188 90, 190 85, 191 84, 191 83, 191 82, 191 81, 190 82, 190 83, 190 87, 190 88, 190 90, 190 92, 190 94, 190 95, 190 102, 190 103, 191 104, 192 105, 195 105, 196 105, 197 105, 198 104, 199 104, 199 103",
            "id": "5"
        },
        {
            "points": "208 81, 208 80, 209 79, 209 78, 209 77, 210 77, 212 76, 213 76, 214 76, 215 75, 216 75, 218 75, 220 76, 221 76, 222 77, 223 78, 224 80, 225 81, 225 82, 225 84, 225 86, 225 87, 225 89, 224 91, 223 93, 222 95, 222 96, 221 98, 220 99, 220 100, 219 101, 219 102, 218 102, 218 101, 219 100, 219 98, 220 97, 221 96, 221 94, 223 93, 225 89, 227 88, 228 86, 229 85, 231 83, 232 82, 236 78, 237 77, 238 77, 238 76, 237 76, 237 77, 233 81, 232 82, 231 83, 230 84, 229 85, 229 88, 229 89, 229 90, 229 91, 229 92, 230 94, 234 97, 235 98, 236 98, 238 99, 239 99, 242 99, 241 99",
            "id": "6"
        },
        {
            "points": "273 79, 273 78, 273 77, 273 76, 272 76, 272 75, 272 74, 272 75, 272 76, 272 77, 272 79, 272 82, 272 84, 273 86, 273 88, 273 90, 274 92, 275 96, 275 98, 276 99, 276 100, 276 101, 276 102, 276 101",
            "id": "7"
        },
        {
            "points": "262 91, 263 91, 264 91, 266 90, 268 90, 270 90, 272 89, 279 88, 281 88, 282 87, 283 87, 284 87, 285 87, 286 87, 287 87, 286 87",
            "id": "8"
        },
        {
            "points": "311 63, 311 62, 311 63, 311 64, 311 66, 311 69, 310 71, 310 74, 310 77, 310 80, 310 83, 310 85, 311 87, 311 89, 311 91, 311 92, 311 94, 311 95, 311 96, 311 97, 311 96, 311 95, 311 94, 311 93, 312 91, 312 90, 312 89, 312 88, 313 87, 313 86, 315 85, 316 84, 317 84, 318 84, 321 83, 322 83, 324 83, 325 83, 326 84, 327 84, 330 86, 331 87, 332 87, 332 88, 333 89, 333 90, 333 91, 333 92, 333 93, 333 94, 333 95, 332 96, 330 97, 329 98, 325 101, 324 101, 322 102, 320 102, 318 102, 317 102, 312 102, 311 101, 310 101, 309 100, 310 100, 311 101, 312 101",
            "id": "9"
        },
        {
            "points": "334 53, 334 52, 334 53, 334 54, 335 54, 336 55, 337 56, 338 57, 339 59, 340 60, 342 62, 343 64, 344 66, 345 68, 346 71, 347 73, 348 76, 349 78, 349 81, 350 83, 350 90, 350 92, 350 95, 349 98, 348 100, 347 105, 346 107, 345 110, 344 112, 343 114, 342 117, 339 121, 338 123, 337 124, 336 125, 335 126, 335 124",
            "id": "10"
        },
        {
            "points": "387 50, 386 50, 385 50, 385 51, 384 52, 383 53, 382 54, 381 55, 380 57, 379 59, 377 60, 376 63, 375 65, 374 67, 374 69, 373 71, 372 74, 371 77, 370 80, 369 82, 369 84, 368 86, 366 96, 366 99, 366 102, 366 104, 368 109, 369 112, 370 114, 372 117, 374 119, 376 121, 378 123, 385 127, 386 127, 387 128",
            "id": "11"
        },
        {
            "points": "418 73, 418 72, 418 71, 417 71, 416 71, 415 71, 413 71, 411 71, 409 72, 407 73, 405 73, 403 74, 402 75, 400 76, 398 78, 397 79, 396 81, 395 82, 395 84, 394 86, 393 87, 392 92, 392 94, 392 95, 392 97, 392 98, 392 100, 395 103, 397 104, 399 105, 401 105, 403 105, 404 105, 406 105, 407 105, 408 105, 408 104",
            "id": "12"
        },
        {
            "points": "429 79, 429 78, 429 77, 429 76, 430 76, 431 75, 432 75, 433 74, 434 74, 436 74, 437 74, 438 74, 439 74, 440 74, 441 74, 441 75, 442 78, 442 80, 442 82, 442 84, 441 86, 440 88, 439 90, 435 94, 434 96, 432 97, 431 99, 430 100, 429 100, 428 101, 427 101, 427 100, 427 99, 428 98, 429 96, 431 94, 433 92, 435 91, 436 90, 438 88, 440 87, 446 81, 447 80, 448 79, 448 78, 448 77, 448 78, 446 79, 445 81, 444 83, 443 84, 442 86, 441 88, 440 93, 441 94, 441 96, 442 97, 443 98, 449 100, 450 100, 452 100, 452 99, 452 98",
            "id": "13"
        },
        {
            "points": "474 73, 474 72, 474 73, 474 74, 474 76, 473 78, 473 80, 472 82, 472 85, 472 87, 471 89, 471 91, 471 92, 471 94, 471 96, 471 97, 471 98, 471 99",
            "id": "14"
        },
        {
            "points": "462 91, 461 91, 461 90, 462 90, 463 90, 465 90, 467 90, 470 89, 472 89, 474 88, 476 88, 478 88, 479 87, 480 87, 479 87",
            "id": "15"
        },
        {
            "points": "510 94, 512 93, 513 93, 513 92, 513 91, 512 91, 512 90, 511 90, 510 90, 509 90, 508 90, 507 90, 506 90, 503 90, 502 91, 500 91, 499 92, 498 93, 496 95, 495 96, 495 97, 494 98, 494 100, 494 101, 494 102, 494 103, 494 104, 494 106, 495 107, 496 108, 497 108, 500 108, 501 108, 502 107, 504 106, 505 105, 507 104, 510 99, 511 98, 512 96, 513 94, 514 92, 515 86, 515 85, 515 83, 516 81, 516 80, 516 76, 516 75, 516 73, 516 72, 516 71, 515 68, 515 67, 515 66, 515 69, 515 70, 515 72, 514 74, 513 80, 513 82, 513 84, 513 87, 513 89, 512 91, 512 96, 512 97, 512 98, 512 99, 512 100, 513 102, 516 103, 517 103, 518 103, 519 103, 520 103, 521 103, 522 103, 523 103, 524 103, 526 103, 525 103, 524 103",
            "id": "16"
        },
        {
            "points": "532 57, 531 57, 531 56, 531 57, 532 57, 533 59, 534 60, 536 61, 537 63, 538 64, 539 66, 544 73, 545 76, 545 79, 546 81, 546 83, 546 86, 546 88, 546 91, 543 99, 542 102, 540 105, 539 108, 538 110, 536 112, 535 114, 534 116, 533 118, 532 119, 532 120, 531 120, 531 118",
            "id": "17"
        },
        {
            "points": "551 62, 550 62, 550 61, 551 61, 552 61, 555 61, 557 61, 559 61, 561 61, 563 61, 564 61, 565 61, 566 61",
            "id": "18"
        },
        {
            "points": "580 65, 580 66, 580 65, 581 65, 583 63, 584 62, 586 60, 587 59, 589 57, 590 54, 591 54, 591 53, 591 52, 592 51, 592 52, 592 53, 592 54, 592 55, 592 57, 592 59, 592 61, 592 63, 592 65, 592 67, 592 70, 592 72, 592 74, 592 79, 592 81, 592 82, 592 84, 591 85, 591 86, 591 87",
            "id": "19"
        }
    ]
```

Output response for above input:

```json
{
    "response_time": "2021-01-22T01:59:08",
    "duration": 0.99,
    "input_type": "strokes",
    "input_file_id": "ISICal19_1201_em_751",
    "output_file_id": "ISICal19_1201_em_751",
    "annotation": "string",
    "mathml": "<mrow><msup><mi xml:id=\"0:\">x</mi>\n<mo xml:id=\"1:\">&prime;</mo>\n</msup>\n<mrow><mo xml:id=\"2:3:\">=</mo>\n<mrow><mo xml:id=\"4:\">(</mo>\n<mrow><mi xml:id=\"5:\">a</mi>\n<mrow><mi xml:id=\"6:\">x</mi>\n<mrow><mo xml:id=\"7:8:\">+</mo>\n<mrow><mi xml:id=\"9:\">b</mi>\n<mrow><mo xml:id=\"10:\">)</mo>\n<mrow><mo xml:id=\"11:\">(</mo>\n<mrow><mi xml:id=\"12:\">c</mi>\n<mrow><mi xml:id=\"13:\">x</mi>\n<mrow><mo xml:id=\"14:15:\">+</mo>\n<mrow><mi xml:id=\"16:\">d</mi>\n<msup><mo xml:id=\"17:\">)</mo>\n<mrow><mo xml:id=\"18:\">-</mo>\n<mn xml:id=\"19:\">1</mn>\n</mrow>\n</msup>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n</mrow>\n",
    "latex": "\\(x^{\\prime}{= \\left( {a{x{+ {b{)\\left( {c{x{+ \\left. d \\right)^{- 1}}}} \\right.}}}}} \\right.}\\)",
    "lg": "O, sym0, x, 1.0, 0\nO, sym1, \\prime, 1.0, 1\nO, sym2, =, 1.0, 2, 3\nO, sym3, (, 1.0, 4\nO, sym4, a, 1.0, 5\nO, sym5, x, 1.0, 6\nO, sym6, +, 1.0, 8, 7\nO, sym7, b, 1.0, 9\nO, sym8, ), 1.0, 10\nO, sym9, (, 1.0, 11\nO, sym10, c, 1.0, 12\nO, sym11, x, 1.0, 13\nO, sym12, +, 1.0, 15, 14\nO, sym13, d, 1.0, 16\nO, sym14, ), 1.0, 17\nO, sym15, -, 1.0, 18\nO, sym16, 1, 1.0, 19\n\n\n# Relations:\nR, sym0, sym1, Sup, 1.0\nR, sym0, sym2, Right, 1.0\nR, sym2, sym3, Right, 1.0\nR, sym3, sym4, Right, 1.0\nR, sym4, sym5, Right, 1.0\nR, sym5, sym6, Right, 1.0\nR, sym6, sym7, Right, 1.0\nR, sym7, sym8, Right, 1.0\nR, sym8, sym9, Right, 1.0\nR, sym9, sym10, Right, 1.0\nR, sym10, sym11, Right, 1.0\nR, sym11, sym12, Right, 1.0\nR, sym12, sym13, Right, 1.0\nR, sym13, sym14, Right, 1.0\nR, sym14, sym15, Sup, 1.0\nR, sym15, sym16, Right, 1.0\n"
}
```

#### Formula image as input

```json
{
  "request_time": "2021-01-22T06:36:34",
  "input_type": "strokes",
  "file_id": "string",
  "annotation": "string",
  "input_image": {
    "base64_img": "string",
    "dpi": 0
  }
}
```

Example:

```json
{
    "request_time": "2021-01-20 11:46",
    "input_type": "image",
    "file_id": "28000104",
    "annotation": "string",
    "input_image": {
        "base64_img": "iVBORw0KGgoAAAANSUhEUgAAAToAAABWCAAAAAB6aAUVAAAEE0lEQVR4nO1b27aEIAiF1vz/L3MeKsW7FlB62g8zUxnqFhTBAfjwIQWRpvRNU/jDUCVubeqUsTB1ykoHP2X5zwJFpJxjEEmTEf5GEMj0jitvIG9p6sSYQ8cgE7ksdTJKdxLnL7zQhZcJARAAoONq/+UMeFXqRJQuWaMD7lalTgwZ/g/uFqVOR+lOmfuDRamTQLBEZLAmdVI+XQqmdmtSJ4GW0q1JnYTS1XfABItSZ4MVqdOb6YI6VqROAkV79WOyIHW6Suc5XZA6XaysdVobiQTrUWcEygTYPeFTxvIsllcAAEy0jqcuddOYkyPWOp7AIACg6RRPVumqkgLqgggyAs3HnaWdMIOlKPY+51xn12xPXZryIbAdxvswbW28wkbMvQ4djUqL6OjhqXWJtU7LnNhbrRdD52TS2a0F0W45YYfBJjonCUHhOKpAKHQIwMO14Mcuc1UIJdBBys+pCMlHxPUMqXHSKa24PoqVpyaTgeWM8wMoKF2+Fe2QfaxdaLTgWG1eHTYYWoAusWDSIZXxqbZcPui06CqdYsttI8rAesHnaGtmTeUxeiC20bry47mUsccJcgar2DWDZeIBpYPtnRuuK5Bk7k25CV2NMHdMAL60zmWkuQkF6M8I8jVgh+AJ/3JCR+oE/Q3/uQP3HeGI2zUOI+qkWk/JZ7kY+StB8nytJ3Vt4dX1fyCupBrfskT3XFcd6eN2NnEb3juLmLpEF8ap9Qr2G+w5d+Siboc+9iRuif9p6ALOo7zoatKdz2rtwLolEmssFPwn8j0qPGYFymKuQsunK0ws/nbdYCn6LgCDr2IBzpwoDFWOtb1KHStXbl03EcT+biUHtUmz1lYEANgqmuBMgbhFlivJPi64CJIkKild2UL2CivLRF8uqdNp4sKs9+lK1W25mwC7F5HrbCPllKUFO4fhZUjVLlg6Nsh2igj4H0H5izn5DZAac7ohk7zJnvVtvogvQ+UWtfKgXTenQcgdhd5XaYrPUdQY4qxb17VIX4Z+nM6ZKD+1ucPtYQPuss25q0Ciu3ArYHhUrugk1CP8rSHOPXcSVfZLRsHhVOEAIHJObjWjrpRWZwA0UKClP0p8t+vT78FijAXYLzUUo28xPKzHg/G6/Wc7LFe7WRQxiEfSYAwX0jqVXud6EqUQKiUnQy91weJ7u98Spva00n152OsYp67i2Va2EsFTCef4caXrpo7NWGNbjVIuY34M5WFvnidCAiChM+XPK12/wXYsEc2unF7xAssrjMx1yD67X4myEfulAHMvUDqp+q2PBr6BujmdkzcwJ0nd430xhgx11u4GvmGg7lBX8ngNoJEMH8V16oh6z1UsinsGy06OvUANjCEw1/1T5gSo+6/M3ehzeOz5H+JOpwtJtg8fGvgDl8gAx7RgZnUAAAAASUVORK5CYII=",
        "dpi": 600
    }
}
```

Output response for above input:

```json
{
    "response_time": "2021-01-22T01:59:45",
    "duration": 0.77,
    "input_type": "image",
    "input_file_id": "28000104",
    "output_file_id": "28000104",
    "annotation": "string",
    "mathml": "<mrow >\n    <msub >\n        <mi  xml:id = \"2:\" >c</mi>\n        <mrow >\n            <mi  xml:id = \"4:6:\" >i</mi>\n            <mrow >\n                <mi  xml:id = \"5:7:\" >j</mi>\n                <mi  xml:id = \"3:\" >k</mi>\n            </mrow>\n        </mrow>\n    </msub>\n    <mrow >\n        <mi  xml:id = \"0:\" >&ne;</mi>\n        <mn  xml:id = \"1:\" >0</mn>\n    </mrow>\n</mrow>\n",
    "latex": "\\(c_{i{jk}}{\\neq 0}\\)",
    "lg": "O, sym0, c, 1.0, 2\nO, sym1, i, 1.0, 4, 6\nO, sym2, j, 1.0, 5, 7\nO, sym3, k, 1.0, 3\nO, sym4, notequal, 1.0, 0\nO, sym5, zero, 1.0, 1\n\n\n# Relations:\nR, sym0, sym1, RSUB, 1.0\nR, sym0, sym4, HORIZONTAL, 1.0\nR, sym1, sym2, HORIZONTAL, 1.0\nR, sym2, sym3, HORIZONTAL, 1.0\nR, sym4, sym5, HORIZONTAL, 1.0\n"
}
```

