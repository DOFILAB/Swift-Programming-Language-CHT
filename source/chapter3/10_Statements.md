> 翻譯：CMW
# 語句
-----------------

本頁包含內容：

- [循環語句](#loop_statements)
- [分支語句](#branch_statements)
- [帶標籤的語句](#labeled_statement)
- [控制傳遞語句](#control_transfer_statements)

在Swift 中，有兩種​​類型的語句：簡單語句和控制流語句。簡單語句是最常見的，用於構造表達式和聲明。控制流語句則用於控製程序執行的流程，Swift 中有三種類型的控制流語句：循環語句、分支語句和控制傳遞語句。

循環語句用於重複執行代碼塊；分支語句用於執行滿足特定條件的代碼塊；控制傳遞語句則用於修改代碼的執行順序。在稍後的敘述中，將會詳細地介紹每一種類型的控制流語句。

是否將分號（`;`）添加到語句的結尾處是可選的。但若要在同一行內寫多條獨立語句，請務必使用分號。

> GRAMMAR OF A STATEMENT

> *statement* → [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)* *;** *opt*

> *statement* → [*declaration*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)* *;** *opt*

> *statement* → [*loop-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop -statement)**;** *opt*

> *statement* → [*branch-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/branch -statement)**;** *opt*

> *statement* → [*labeled-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/labeled -statement)

> *statement* → [*control-transfer-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /control-transfer-statement)**;** *opt*

> *statement* → [*statment*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement) [ *statements*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements)**;** *opt *

<a name="loop_statements"></a>
## 循環語句

取決於特定的循環條件，循環語句允許重複執行代碼塊。 Swift 提供四種類型的循環語句：`for`語句、`for-in`語句、`while`語句和`do-whil​​e`語句。

通過`break`語句和`continue`語句可以改變循環語句的控制流。有關這兩條語句，詳情參見[Break 語句](#break_statement)和[Continue 語句](#continue_statement)。

> GRAMMAR OF A LOOP STATEMENT

> *loop-statement* → [*for-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /for-statement)

> *loop-statement* → [*for-in-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift /grammar/for-in-statement)

> *loop-statement* → [*while-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /while-statement)

> *loop-statement* → [*do-whil​​e-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift /grammar/do-whil​​e-statement)

### For 語句

`for`語句允許在重複執行代碼塊的同時，遞增一個計數器。

`for`語句的形式如下：

```swift
for `initialzation`; `condition`; `increment` {
`statements`
}
```

*initialzation*、*​​condition* 和*increment* 之間的分號，以及包圍循環體*statements* 的大括號都是不可省略的。

`for`語句的執行流程如下：

1. *initialzation* 只會被執行一次，通常用於聲明和初始化在接下來的循環中需要使用的變量。

2. 計算 *condition* 表達式：
如果為`true`，*statements* 將會被執行，然後轉到第3步。如果為`false`，*statements* 和*increment* 都不會被執行，`for`至此執行完畢。

3. 計算*increment* 表達式，然後轉到第2步。

定義在*initialzation* 中的變量僅在`for`語句的作用域以內有效。 *condition* 表達式的值的類型必須遵循`LogicValue`協議。

> GRAMMAR OF A FOR STATEMENT

> *for-statement* → **for** [*for-init*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#// apple_ref/swift/grammar/for-init) *opt* **;** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions. html#//apple_ref/swift/grammar/expression) *opt* **;** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ Expressions.html#//apple_ref/swift/grammar/expression) *opt* [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations .html#//apple_ref/swift/grammar/code-block)

> *for-statement* → **for (** [*for-init*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#/ /apple_ref/swift/grammar/for-init) *opt* **;** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions .html#//apple_ref/swift/grammar/expression) *opt* **;** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language /Expressions.html#//apple_ref/swift/grammar/expression) *opt* **)** [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift /Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)

> *for-statement* → [*variable-declaration*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar /variable-declaration) | [*expression-list*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/ expression-list)

### For-In 語句

`for-in`語句允許在重複執行代碼塊的同時，迭代集合（或遵循`Sequence`協議的任意類型）中的每一項。

`for-in`語句的形式如下：

```swift
for `item` in `collection` {
`statements`
}
```

`for-in`語句在循環開始前會調用*collection* 表達式的`generate`方法來獲取一個生成器類型（這是一個遵循`Generator`協議的類型）的值。接下來循環開始，調用*collection* 表達式的`next`方法。如果其返回值不是`None`，它將會被賦給*item*，然後執行*statements*，執行完畢後回到循環開始處；否則，將不會賦值給*item* 也不會執行*statements *，`for-in`至此執行完畢。

> GRAMMAR OF A FOR-IN STATEMENT

> *for-in-statement* → **for** [*pattern*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#// apple_ref/swift/grammar/pattern) **in** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref /swift/grammar/expression) [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar /code-block)

### While 語句

`while`語句允許重複執行代碼塊。

`while`語句的形式如下：

```swift
while `condition` {
`statements`
}
```

`while`語句的執行流程如下：

1. 計算 *condition* 表達式：
如果為真`true`，轉到第2步。如果為`false`，`while`至此執行完畢。

2. 執行 *statements* ，然後轉到第1步。

由於*condition* 的值在*statements* 執行前就已計算出，因此`while`語句中的*statements* 可能會被執行若干次，也可能不會被執行。

*condition* 表達式的值的類型必須遵循`LogicValue`協議。同時，*condition* 表達式也可以使用可選綁定，詳情參見[可選綁定](../chapter2/01_The_Basics.html#optional_binding)。

> GRAMMAR OF A WHILE STATEMENT

> *while-statement* → **while** [*while-condition*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#// apple_ref/swift/grammar/while-condition) [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/ swift/grammar/code-block)

> *while-condition* → [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression ) | [*declaration*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)

### Do-While 語句

`do-whil​​e`語句允許代碼塊被執行一次或多次。

`do-whil​​e`語句的形式如下：

```swift
do {
`statements`
} while `condition`
```

`do-whil​​e`語句的執行流程如下：

1. 執行 *statements*，然後轉到第2步。

2. 計算 *condition* 表達式：
如果為`true`，轉到第1步。如果為`false`，`do-whil​​e`至此執行完畢。

由於*condition* 表達式的值是在*statements* 執行後才計算出，因此`do-whil​​e`語句中的*statements* 至少會被執行一次。

*condition* 表達式的值的類型必須遵循`LogicValue`協議。同時，*condition* 表達式也可以使用可選綁定，詳情參見[可選綁定](../chapter2/01_The_Basics.html#optional_binding)。

> GRAMMAR OF A DO-WHILE STATEMENT

> *do-whil​​e-statement* → **do** [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html# //apple_ref/swift/grammar/code-block) **while** [*while-condition*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements .html#//apple_ref/swift/grammar/while-condition)

<a name="branch_statements"></a>
## 分支語句

取決於一個或者多個條件的值，分支語句允許程序執行指定部分的代碼。顯然，分支語句中條件的值將會決定如何分支以及執行哪一塊代碼。 Swift 提供兩種類型的分支語句：`if`語句和`switch`語句。

`switch`語句中的控制流可以用`break`語句修改，詳情請見[Break 語句](#break_statement)。

> GRAMMAR OF A BRANCH STATEMENT

> *branch-statement* → [*if-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /if-statement)

> *branch-statement* → [*switch-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /switch-statement)

### If 語句

取決於一個或多個條件的值，`if`語句將決定執行哪一塊代碼。

`if`語句有兩種標準形式，在這兩種形式裡都必須有大括號。

第一種形式是當且僅當條件為真時執行代碼，像下面​​這樣：

```swift
if `condition` {
`statements`
}
```

第二種形式是在第一種形式的基礎上添加*else 語句*，當只有一個else 語句時，像下面這樣：

```swift
if `condition` {
`statements to execute if condition is true`
} else {
`statements to execute if condition is false`
}
```

同時，else 語句也可包含`if`語句，從而形成一條鏈來測試更多的條件，像下面這樣：

```swift
if `condition 1` {
`statements to execute if condition 1 is true`
} else if `condition 2` {
`statements to execute if condition 2 is true`
}
else {
`statements to execute if both conditions are false`
}
```

`if`語句中條件的值的類型必須遵循`LogicValue`協議。同時，條件也可以使用可選綁定，詳情參見[可選綁定](../chapter2/01_The_Basics.html#optional_binding)。

> GRAMMAR OF AN IF STATEMENT

> *if-statement* → **if** [*if-condition*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#// apple_ref/swift/grammar/if-condition) [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/ swift/grammar/code-block) [*else-clause*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/ grammar/else-clause) *opt*

> *if-condition* → [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression ) | [*declaration*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)

> *else-clause* → **else** [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#// apple_ref/swift/grammar/code-block) | **else** [*if-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements. html#//apple_ref/swift/grammar/if-statement) *opt*

### Switch 語句

取決於`switch`語句的*控製表達式（control expression）*，`switch`語句將決定執行哪一塊代碼。

`switch`語句的形式如下：

```swift
switch `control expression` {
case `pattern 1`:
`statements`
case `pattern 2` where `condition`:
`statements`
case `pattern 3` where `condition`,
`pattern 4` where `condition`:
`statements`
default:
`statements`
}
```

`switch`語句的*控製表達式（control expression）*會首先被計算，然後與每一個case 的模式（pattern）進行匹配。如果匹配成功，程序將會執行對應的case 分支裡的*statements*。另外，每一個case 分支都不能為空，也就是說在每一個case 分支中至少有一條語句。如果你不想在匹配到的case 分支中執行代碼，只需在該分支裡寫一條`break`語句即可。

可以用作控製表達式的值是十分靈活的，除了標量類型(scalar types，如`Int`、`Character`)外，你可以使用任何類型的值，包括浮點數、字符串、元組、自定義類的實例和可選（optional）類型，甚至是枚舉類型中的成員值和指定的範圍(range)等。關於在`switch`語句中使用這些類型，詳情參見[控制流](../chapter2/05_Control_Flow.html)一章的[Switch](../chapter2/05_Control_Flow.html#switch)。

你可以在模式後面添加一個起保護作用的表達式(guard expression)。 *起保護作用的表達式*是這樣構成的：關鍵字`where`後面跟著一個作為額外測試條件的表達式。因此，當且僅當*控製表達式*匹配一個*case*的某個模式且起保護作用的表達式為真時，對應case 分支中的*statements* 才會被執行。在下面的例子中，*控製表達式*只會匹配含兩個相等元素的元組，如`(1, 1)`：

```swift
case let (x, y) where x == y:
```

正如上面這個例子，也可以在模式中使用`let`（或`var`）語句來綁定常量（或變量）。這些常量（或變量）可以在其對應的起保護作用的表達式和其對應的*case*塊裡的代碼中引用。但是，如果case 中有多個模式匹配控製表達式，那麼這些模式都不能綁定常量（或變量）。

`switch`語句也可以包含默認（`default`）分支，只有其它case 分支都無法匹配控製表達式時，默認分支中的代碼才會被執行。一個`switch`語句只能有一個默認分支，而且必須在`switch`語句的最後面。

儘管模式匹配操作實際的執行順序，特別是模式的計算順序是不可知的，但是Swift 規定`switch`語句中的模式匹配的順序和書寫源代碼的順序保持一致。因此，當多個模式含有相同的值且能夠匹配控製表達式時，程序只會執行源代碼中第一個匹配的case 分支中的代碼。

#### Switch 語句必須是完備的

在Swift 中，`switch`語句中控製表達式的每一個可能的值都必須至少有一個case 分支與之對應。在某些情況下（例如，表達式的類型是`Int`），你可以使用默認塊滿足該要求。

#### 不存在隱式的貫穿(fall through)

當匹配的case 分支中的代碼執行完畢後，程序會終止`switch`語句，而不會繼續執行下一個case 分支。這就意味著，如果你想執行下一個case 分支，需要顯式地在你需要的case 分支裡使用`fallthrough`語句。關於`fallthrough`語句的更多信息，詳情參見[Fallthrough 語句](#fallthrough_statement)。

> GRAMMAR OF A SWITCH STATEMENT

> *switch-statement* → **switch** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/ swift/grammar/expression) **{** [*switch-cases*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref /swift/grammar/switch-cases) *opt* **}**

> *switch-cases* → [*switch-case*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /switch-case) [*switch-cases*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch -cases) *opt*

> *switch-case* → [*case-label*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /case-label) [*statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements) | [*default-label*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/default-label) [* statements*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements)

> *switch-case* → [*case-label*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /case-label) **;** | [*default-label*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref /swift/grammar/default-label) **;**

> *case-label* → **case** [*case-item-list*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html# //apple_ref/swift/grammar/case-item-list) **:**

> *case-item-list* → [*pattern*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar /pattern) [*guard-clause*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-clause ) *opt* | [*pattern*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern) [ *guard-clause*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-clause) *opt* , [*case-item-list*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-item -list)

> *default-label* → **default :**

> *guard-clause* → **where** [*guard-expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#// apple_ref/swift/grammar/guard-expression)

> *guard-expression* → [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression )

<a name="labeled_statement"></a>
<a name="control_transfer_statements"></a> 帶標籤的語句

你可以在循環語句或`switch`語句前面加上*標籤*，它由標籤名和緊隨其後的冒號(:)組成。在`break`和`continue`後面跟上標籤名可以顯式地在循環語句或`switch`語句中更改控制流，把控制權傳遞給指定標籤標記的語句。關於這兩條語句用法，詳情參見[Break 語句](#break_statement)和[Continue 語句](#continue_statement)。

標籤的作用域是該標籤所標記的語句之後的所有語句。你可以不使用帶標籤的語句，但只要使用它，標籤名就必唯一。

關於使用帶標籤的語句的例子，詳情參見[控制流](../chapter2/05_Control_Flow.html)一章的[帶標籤的語句](../chapter2/05_Control_Flow.html#labeled_statements)。

> GRAMMAR OF A LABELED STATEMENT

> *labeled-statement* → [*statement-label*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /statement-label) [*loop-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop -statement) | [*statement-label*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement- label) [*switch-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)

> *statement-label* → [*label-name*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar /label-name) **:**

> *label-name* → [*identifier*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier )


## 控制傳遞語句

通過無條件地把控制權從一片代碼傳遞到另一片代碼，控制傳遞語句能夠改變代碼執行的順序。 Swift 提供四種類型的控制傳遞語句：`break`語句、`continue`語句、`fallthrough`語句和`return`語句。

> GRAMMAR OF A CONTROL TRANSER STATEMENT

> *control-transfer-statement* → [*break-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift /grammar/break-statement)

> *control-transfer-statement* → [*continue-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift /grammar/continue-statement)

> *control-transfer-statement* → [*fallthrough-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift /grammar/fallthrough-statement)

> *control-transfer-statement* → [*return-statement*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift /grammar/return-statement)

<a name="break_statement"></a>
### Break 語句

`break`語句用於終止循環或`switch`語句的執行。使用`break`語句時，可以只寫`break`這個關鍵詞，也可以在`break`後面跟上標籤名（label name），像下面這樣：

```swift
break
break `label name`
```

當`break`語句後面帶標籤名時，可用於終止由這個標籤標記的循環或`switch`語句的執行。

而當只寫`break`時，則會終止`switch`語句或上下文中包含`break`語句的最內層循環的執行。

在這兩種情況下，控制權都會被傳遞給循環或`switch`語句外面的第一行語句。

關於使用`break`語句的例子，詳情參見[控制流](../chapter2/05_Control_Flow.html)一章的[Break](../chapter2/05_Control_Flow.html#break) 和[帶標籤的語句] (../chapter2/05_Control_Flow.html#labeled_statements)。

> GRAMMAR OF A BREAK STATEMENT

> *break-statement* → **break** [*label-name*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#// apple_ref/swift/grammar/label-name) *opt*

<a name="continue_statement"></a>
### Continue 語句

`continue`語句用於終止循環中當前迭代的執行，但不會終止該循環的執行。使用`continue`語句時，可以只寫`continue`這個關鍵詞，也可以在`continue`後面跟上標籤名（label name），像下面這樣：

```swift
continue
continue `label name`
```

當`continue`語句後面帶標籤名時，可用於終止由這個標籤標記的循環中當前迭代的執行。

而當只寫`break`時，可用於終止上下文中包含`continue`語句的最內層循環中當前迭代的執行。

在這兩種情況下，控制權都會被傳遞給循環外面的第一行語句。

在`for`語句中，`continue`語句執行後，*increment* 表達式還是會被計算，這是因為每次循環體執行完畢後*increment* 表達式都會被計算。

關於使用`continue`語句的例子，詳情參見[控制流](../chapter2/05_Control_Flow.html)一章的[Continue](../chapter2/05_Control_Flow.html#continue) 和[帶標籤的語句] (../chapter2/05_Control_Flow.html#labeled_statements)。

> GRAMMAR OF A CONTINUE STATEMENT

> *continue-statement* → **continue** [*label-name*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#// apple_ref/swift/grammar/label-name) *opt*

<a name="fallthrough_statement"></a>
### Fallthrough 語句

`fallthrough`語句用於在`switch`語句中傳遞控制權。 `fallthrough`語句會把控制權從`switch`語句中的一個case 傳遞給下一個case 。這種傳遞是無條件的，即使下一個case 的模式與`switch`語句的控製表達式的值不匹配。

`fallthrough`語句可出現在`switch`語句中的任意case 裡，但不能出現在最後一個case 分支中。同時，`fallthrough`語句也不能把控制權傳遞給使用了可選綁定的case 分支。

關於在`switch`語句中使用`fallthrough`語句的例子，詳情參見[控制流](../chapter2/05_Control_Flow.html)一章的[控制傳遞語句](../chapter2/05_Control_Flow.html#control_transfer_statements )。

> GRAMMAR OF A FALLTHROUGH STATEMENT

> *continue-statement* → **fallthrough**

### Return 語句

`return`語句用於在函數或方法的實現中將控制權傳遞給調用者，接著程序將會從調用者的位置繼續向下執行。

使用`return`語句時，可以只寫`return`這個關鍵詞，也可以在`return`後面跟上表達式，像下面這樣：

```swift
return
return `expression`
```

當`return`語句後面帶錶達式時，表達式的值將會返回給調用者。如果表達式值的類型與調用者期望的類型不匹配，Swift 則會在返回表達式的值之前將表達式值的類型轉換為調用者期望的類型。

而當只寫`return`時，僅僅是將控制權從該函數或方法傳遞給調用者，而不返回一個值。 （這就是說，該函數或方法的返回類型為`Void`或`()`）

> GRAMMAR OF A RETURN STATEMENT

> *return-statement* → **return** [*expression*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/ swift/grammar/expression) *opt*
