> 翻譯：CMW
# 詞法結構
-----------------

本頁包含內容：

- [空白與註釋（*Whitespace and Comments*）](#whitespace_and_comments)
- [標識符（*Identifiers*）](#identifiers)
- [關鍵字（*Keywords*）](#keywords)
- [字面量（*Literals*）](#literals)
- [運算符（*Operators*）](#operators)

Swift 的“詞法結構（*lexical structure*）”描述瞭如何在該語言中用字符序列構建合法標記，組成該語言中最底層的代碼塊，並在之後的章節中用於描述語言的其他部分。

通常，標記在隨後介紹的語法約束下，由Swift 源文件的輸入文本中提取可能的最長子串生成。這種方法稱為“最長匹配項（*longest match*）”，或者“最大適合”（*maximal munch*）。

<a name="whitespace_and_comments"></a>
## 空白與註釋

空白（*whitespace*）有兩個用途：分隔源文件中的標記和區分運算符屬於前綴還是後綴，（參見[運算符](https://developer.apple.com/library/prerelease/ios/documentation /Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/doc/uid/TP40014097-CH30-XID_871)）在其他情況下則會被忽略。以下的字符會被當作空白：空格（*space*）（U+0020）、換行符（*line feed*）（U+000A）、回車符（*carriage return*）（U+000D）、水平tab（*horizo​​ntal tab*）（U+0009）、垂直tab（*vertical tab*）（U+000B）、換頁符（*form feed*）（U+000C）以及空（*null*）（ U+0000）。

註釋（*comments*）被編譯器當作空白處理。單行註釋由 `//` 開始直到該行結束。多行註釋由 `/*` 開始，以 `*/` 結束。可以嵌套註釋，但注意註釋標記必須匹配。

<a name="identifiers"></a>
## 標識符

標識符（*identifiers*）可以由以下的字符開始：大寫或小寫的字母`A` 到`Z`、下劃線`_`、基本多語言面（*Basic Multilingual Plane*）中的Unicode 非組合字符以及基本多語言面以外的非專用區（*Private Use Area*）字符。首字符之後，標識符允許使用數字和Unicode 字符組合。

使用保留字（*reserved word*）作為標識符，需要在其前後增加反引號<code>\`</code>。例如，<code>class</code> 不是合法的標識符，但可以使用<code>\`class\`</code>。反引號不屬於標識符的一部分，<code>\`x\`</code> 和`x` 表示同一標識符。

閉包（*closure*）中如果沒有明確指定參數名稱，參數將被隱式命名為<code>$0</code>、<code>$1</code>、<code>$2</code>.. . 這些命名在閉包作用域內是合法的標識符。

> 標識符語法
>
> *identifier* → [identifier-head](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier-head ) [identifier-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier-characters) *opt*
>
> *identifier* → \` [identifier-head](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier -head) [identifier-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier-characters) * opt* \`
>
> *identifier* → [implicit-parameter-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/implicit -parameter-name)
>
> *identifier-list* → [identifier](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier)​​ | [identifier](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier)​​ , [identifier-list](https ://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier-list)
>
> *identifier-head* → A 到Z 大寫或小寫字母
>
> *identifier-head* → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, 或U+00B7–U+00BA
>
> *identifier-head* → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, 或U+00F8–U+00FF
>
> *identifier-head* → U+0100–U+02FF, U+0370–U+167F, U+1681–U+180D, 或U+180F–U+1DBF
>
> *identifier-head* → U+1E00–U+1FFF
>
> *identifier-head* → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, 或U+2060–U+206F
>
> *identifier-head* → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, 或U+2776–U+2793
>
> *identifier-head* → U+2C00–U+2DFF 或U+2E80–U+2FFF
>
> *identifier-head* → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, 或U+3040–U+D7FF
>
> *identifier-head* → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, 或U+FE30–U+FE44
>
> *identifier-head* → U+FE47–U+FFFD
>
> *identifier-head* → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, 或U+40000–U+4FFFD
>
> *identifier-head* → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, 或U+80000–U+8FFFD
>
> *identifier-head* → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, 或U+C0000–U+CFFFD
>
> *identifier-head* → U+D0000–U+DFFFD 或U+E0000–U+EFFFD
>
> *identifier-character* → 數字 0 到 9
>
> *identifier-character* → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, or U+FE20–U+FE2F
>
> *identifier-character* → [identifier-head](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier -head)
>
> *identifier-characters* → [identifier-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier -character) [identifier-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier-characters) * opt*
>
> *implicit-parameter-name* → **$** [decimal-digits](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#// apple_ref/swift/grammar/decimal-digits)

<a name="keywords"></a>
## 關鍵字

被保留的關鍵字（*keywords*）不允許用作標識符，除非被反引號轉義，參見[標識符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/ Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/doc/uid/TP40014097-CH30-XID_796)。

* **用作聲明的關鍵字：** *class*、*deinit*、*enum*、*extension*、*​​func*、*import*、*init*、*let*、*protocol*、*static *、*struct*、*subscript*、*typealias*、*var*

* **用作語句的關鍵字：** *break*、*case*、*continue*、*default*、*do*、*else*、*fallthrough*、*if*、*in*、*for *、*return*、*switch*、*where*、*while*

* **用作表達和類型的關鍵字：** *as*、*dynamicType*、*is*、*new*、*super*、*self*、*Self*、*Type*、*\_\ _COLUMN\_\_*、*\_\_FILE\_\_*、*\_\_FUNCTION\_\_*、*\_\_LINE\_\_*

* **特定上下文中被保留的關鍵字：** *associativity*、*didSet*、*get*、*infix*、*inout*、*left*、*mutating*、*none*、*nonmutating*、 *operator*、*override*、*postfix*、*precedence*、*prefix*、*right*、*set*、*unowned*、*unowned(safe)*、*unowned(unsafe)*、*weak*、 *willSet*，這些關鍵字在特定上下文之外可以被用於標識符。

<a name="literals"></a>
## 字面量

字面值表示整型、浮點型數字或文本類型的值，舉例如下：

```swift
42 // 整型字面量
3.14159 // 浮點型字面量
"Hello, world!" // 文本型字面量
```

> 字面量語法
>
> *literal* → [integer-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/integer-literal ) | [floating-point-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/floating-point- literal) | [string-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/string-literal)

### 整型字面量

整型字面量（*integer literals*）表示未指定精度整型數的值。整型字面量默認用十進製表示，可以加前綴來指定其他的進制，二進製字面量加`0b`，八進製字面量加`0o`，十六進製字面量加`0x`。

十進製字面量包含數字 `0` 至 `9`。二進製字面量只包含`0` 或`1`，八進製字面量包含數字`0` 至`7`，十六進製字面量包含數字`0` 至`9` 以及字母`A` 至`F` （大小寫均可）。

負整數的字面量在數字前加減號`-`，比如`-42`。

允許使用下劃線`_` 來增加數字的可讀性，下劃線不會影響字面量的值。整型字面量也可以在數字前加`0`，同樣不會影響字面量的值。

```swift
1000_000 // 等於 1000000
005 // 等於 5
```

除非特殊指定，整型字面量的默認類型為Swift 標準庫類型中的`Int`。 Swift 標準庫還定義了其他不同長度以及是否帶符號的整數類型，請參考[整數類型](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics. html#//apple_ref/doc/uid/TP40014097-CH5-XID_411)。

> 整型字面量語法
>
> *integer-literal* → [binary-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/binary -literal)
>
> *integer-literal* → [octal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/octal -literal)
>
> *integer-literal* → [decimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal -literal)
>
> *integer-literal* → [hexadecimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal -literal)
>
> *binary-literal* → **0b** [binary-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/ swift/grammar/binary-digit) [binary-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/ grammar/binary-literal-characters) *opt*
>
> *binary-digit* → 數字 0 或 1
>
> *binary-literal-character* → [binary-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /binary-digit) | _
>
> *binary-literal-characters* → [binary-literal-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/binary-literal-character) [binary-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/binary-literal-characters) *opt*
>
> *octal-literal* → **0o** [octal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/ swift/grammar/octal-digit) [octal-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/ grammar/octal-literal-characters) *opt*
>
> *octal-digit* → 數字 0 至 7
>
> *octal-literal-character* → [octal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /octal-digit) | _
>
> *octal-literal-characters* → [octal-literal-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/octal-literal-character) [octal-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/octal-literal-characters) *opt*
>
> *decimal-literal* → [decimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal -digit) [decimal-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal-literal -characters) *opt*
>
> *decimal-digit* → 數字 0 至 9
>
> *decimal-digits* → [decimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal -digit) [decimal-digits](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal-digits) * opt*
>
> *decimal-literal-character* → [decimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /decimal-digit) | _
>
> *decimal-literal-characters* → [decimal-literal-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/decimal-literal-character) [decimal-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/decimal-literal-characters) *opt*
>
> *hexadecimal-literal* → **0x** [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/ swift/grammar/hexadecimal-digit) [hexadecimal-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/ grammar/hexadecimal-literal-characters) *opt*
>
> *hexadecimal-digit* → 數字0 到9, a 到f, 或A 到 F
>
> *hexadecimal-literal-character* → [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /hexadecimal-digit) | _
>
> *hexadecimal-literal-characters* → [hexadecimal-literal-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/hexadecimal-literal-character) [hexadecimal-literal-characters](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift /grammar/hexadecimal-literal-characters) *opt*

### 浮點型字面量

浮點型字面量（*floating-point literals*）表示未指定精度浮點數的值。

浮點型字面量默認用十進製表示（無前綴），也可以用十六進製表示（加前綴`0x`）。

十進制浮點型字面量（*decimal floating-point literals*）由十進制數字串後跟小數部分或指數部分（或兩者皆有）組成。十進制小數部分由小數點`.` 後跟十進制數字串組成。指數部分由大寫或小寫字母`e` 後跟十進制數字串組成，這串數字表示`e` 之前的數量乘以10 的幾次方。例如：`1.25e2` 表示`1.25 ⨉ 10^2`，也就是`125.0`；同樣，`1.25e－2` 表示`1.25 ⨉ 10^－2`，也就是`0.0125`。

十六進制浮點型字面量（*hexadecimal floating-point literals*）由前綴`0x` 後跟可選的十六進制小數部分以及十六進制指數部分組成。十六進制小數部分由小數點後跟十六進制數字串組成。指數部分由大寫或小寫字母`p` 後跟十進制數字串組成，這串數字表示`p` 之前的數量乘以2 的幾次方。例如：`0xFp2` 表示`15 ⨉ 2^2`，也就是`60`；同樣，`0xFp-2` 表示`15 ⨉ 2^-2`，也就是`3.75`。

與整型字面量不同，負的浮點型字面量由一元運算符減號`-` 和浮點型字面量組成，例如`-42.0`。這代表一個表達式，而不是一個浮點整型字面量。

允許使用下劃線`_` 來增強可讀性，下劃線不會影響字面量的值。浮點型字面量也可以在數字前加`0`，同樣不會影響字面量的值。

```swift
10_000.56 // 等於 10000.56
005000.76 // 等於 5000.76
```

除非特殊指定，浮點型字面量的默認類型為Swift 標準庫類型中的`Double`，表示64位浮點數。 Swift 標準庫也定義`Float` 類型，表示32位浮點數。

> 浮點型字面量語法
>
> *floating-point-literal* → [decimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /decimal-literal) [decimal-fraction](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal-fraction ) *opt* [decimal-exponent](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal-exponent) *opt*
>
> *floating-point-literal* → [hexadecimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /hexadecimal-literal) [hexadecimal-fraction](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-fraction ) *opt* [hexadecimal-exponent](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-exponent)
>
> *decimal-fraction* → . [decimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/ decimal-literal)
>
> *decimal-exponent* → [floating-point-e](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /floating-point-e) [sign](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/sign) * opt* [decimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/decimal-literal)
>
> *hexadecimal-fraction* → . [hexadecimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/ hexadecimal-literal) *opt*
>
> *hexadecimal-exponent* → [floating-point-p](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /floating-point-p) [sign](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/sign) * opt* [hexadecimal-literal](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-literal)
>
> *floating-point-e* → **e­** | **E**­
>
> *floating-point-p* → **p**­ | **P**­
>
> *sign* → **+**­ | **-**­



### 文本型字面量

文本型字面量（*string literal*）由雙引號中的字符串組成，形式如下：

"characters"

文本型字面量中不能包含未轉義的雙引號`"`、未轉義的反斜線`\`、回車符（*carriage return*）或換行符（*line feed*）。

可以在文本型字面量中使用的轉義特殊符號如下：

* 空字符（Null Character）`\0`
* 反斜線（Backslash）`\\`
* 水平 Tab （Horizo​​ntal Tab）`\t`
* 換行符（Line Feed）`\n`
* 回車符（Carriage Return）`\r`
* 雙引號（Double Quote）`\"`
* 單引號（Single Quote）`\'`

字符也可以用以下方式表示：

* `\x` 後跟兩位十六進制數字
* `\u` 後跟四位十六進制數字
* `\U` 後跟八位十六進制數字

後跟的數字表示一個 Unicode 碼點。

文本型字面量允許在反斜線小括號`\()` 中插入表達式的值。插入表達式（*interpolated expression*）不能包含未轉義的雙引號`"`、反斜線`\`、回車符或者換行符。表達式值的類型必須在*String* 類中有對應的初始化方法。

例如，以下所有文本型字面量的值相同：

```swift
"1 2 3"
"1 2 \(3)"
"1 2 \(1 + 2)"
var x = 3; "1 2 \(x)"
```

文本型字面量的默認類型為 `String`。組成字符串的字符類型為 `Character`。更多有關`String` 和`Character` 的信息請參照[字符串和字符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html#/ /apple_ref/doc/uid/TP40014097-CH7-XID_368)。

> 文本型字面量語法
>
> *string-literal* → **"** [quoted-text](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/ swift/grammar/quoted-text) **"**
>
> *quoted-text* → [quoted-text-item](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /quoted-text-item) [quoted-text](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/quoted -text) *opt*
>
> *quoted-text-item* → [escaped-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /escaped-character)
>
> *quoted-text-item* → **\(** [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref /swift/grammar/expression) **)**
>
> *quoted-text-item* → 除`"`、`\`、`U+000A` 或`U+000D` 以外的任何Unicode 擴展字符集
>
> *escaped-character* → **\0** | **\\** | **\t** | **\n** | **\r** | **\"** | * *\'**
>
> *escaped-character* → **\x** [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref /swift/grammar/hexadecimal-digit) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /hexadecimal-digit)
>
> *escaped-character* → **\u** [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref /swift/grammar/hexadecimal-digit) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /hexadecimal-digit) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit ) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit)
>
> *escaped-character* → **\U** [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref /swift/grammar/hexadecimal-digit) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar /hexadecimal-digit) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit ) [hexadecimal-digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit) [hexadecimal- digit](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit) [hexadecimal-digit](https ://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit) [hexadecimal-digit](https://developer .apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit) [hexadecimal-digit](https://developer.apple.com /library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/hexadecimal-digit)

<a name="operators"></a>
## 運算符

Swift 標準庫定義了許多可供使用的運算符，其中大部分在[基礎運算符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/BasicOperators.html #//apple_ref/doc/uid/TP40014097-CH6-XID_70) 和[高級運算符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html# //apple_ref/doc/uid/TP40014097-CH27-XID_28) 中進行了闡述。這裡將描述哪些字​​符能用作運算符。

運算符由一個或多個以下字符組成：
`/`、`=`、`-`、`+`、`!`、`*`、`%`、`<`、`>`、`&`、`|`、`^`、`~ `、`.`。也就是說，標記`=`, `->`、`//`、`/*`、`*/`、`.` 以及一元前綴運算符`&` 屬於保留字，這些標記不能被重寫或用於自定義運算符。

運算符兩側的空白被用來區分該運算符是否為前綴運算符（*prefix operator*）、後綴運算符（*postfix operator*）或二元運算符（*binary operator*）。規則總結如下：

* 如果運算符兩側都有空白或兩側都無空白，將被看作二元運算符。例如：`a+b` 和`a + b` 中的運算符`+` 被看作二元運算符。

* 如果運算符只有左側空白，將被看作前綴一元運算符。例如`a ++b` 中的`++` 被看作前綴一元運算符。

* 如果運算符只有右側空白，將被看作後綴一元運算符。例如`a++ b` 中的`++` 被看作後綴一元運算符。

* 如果運算符左側沒有空白並緊跟`.`，將被看作後綴一元運算符。例如`a++.b` 中的`++` 被看作後綴一元運算符（同理， `a++ . b` 中的`++` 是後綴一元運算符而`a ++ .b` 中的` ++` 不是）.

鑑於這些規則，運算符前的字符`(`、`[` 和`{` ；運算符後的字符`)`、`]` 和`}` 以及字符`,`、`;` 和`:`都將用於空白檢測。

以上規則需注意一點，如果運算符`!` 或`?` 左側沒有空白，則不管右側是否有空白都將被看作後綴運算符。如果將`?` 用作可選類型（*optional type*）修飾，左側必須無空白。如果用於條件運算符`? :`，必須兩側都有空白。

在特定構成中，以`<` 或`>` 開頭的運算符會被分離成兩個或多個標記，剩餘部分以同樣的方式會被再次分離。因此，在`Dictionary<String, Array<Int>>` 中沒有必要添加空白來消除閉合字符`>` 的歧義。在這個例子中， 閉合字符​​`>` 被看作單字符標記，而不會被誤解為移位運算符`>>`。

要學習如何自定義新的運算符，請參考[自定義操作符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html#//apple_ref /doc/uid/TP40014097-CH27-XID_48) 和[運算符聲明](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/ doc/uid/TP40014097-CH34-XID_644)。學習如何重寫現有運算符，請參考[運算符方法​​](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html#//apple_ref/doc /uid/TP40014097-CH27-XID_43)。

> 運算符語法
>
> *operator* → [operator-character](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/operator-character ) [operator](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/operator) *opt*
>
> *operator-character* → **/** | **=** | **-** | **+** | **!** | ***** | **%** | * *<** | **>** | **&** | **|** | **^** | **~** | **.**
>
> *binary-operator* → [operator](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/operator)
>
> *prefix-operator* → [operator](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/operator)
>
> *postfix-operator* → [operator­](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/operator)
