layout: true
.footer[
Software quality manual
]

???
---

# Software quality manual

> An example from the real world

???
---

Title: C coding rules

Application date:

Issued by:

Verified by:

Approved by:

Reason for up dating: 

???
---

## Scope of this document

These rules shall be applied for embedded software coded in C.

C code programming must / shall be MISRA C 2004 compliant.

???
---

## Architecture

All software parts will be described at an architecture level, grouped in scopes:

  - Application layer
  - Data presentation layer
  - Hardware abstraction layer

???
---

layout: true
.footer[
Naming rules
]

???
---

## Naming rules 

English language shall be used in sources (comments) and any
accompanying documentation.

???
---

### Files

Each software module includes the following files:

  - Source file (.c)
  - Header file (.h)
  - Configuration source file (.c)
  - Configuration header file (.h)

???
---

### Files

The naming of the module file shall use the following rule:

`[Lll][Mmm][_p]_[Name].c/.h`

  - [Lll]: architecture level
  - [Mmm]: module short name
  - [_p]: (if present) configuration file
  - [Name]: descriptive name

???
---

### Types / Enums: Basic Types 

Following MISRA prescriptions the usage of native types
like “int” or “char” is forbidden, use precise typedefs instead.

???
---

### Types / Enums: Basic Types 

```c
typedef            	void  	VOID;
typedef    signed  	char  	S8;
typedef    signed  	short 	S16;
typedef    signed  	int   	S32;
typedef  unsigned  	char  	U8;
typedef  unsigned  	short 	U16;
typedef  unsigned  	int   	U32;
```

???
---

### Types: Private Types

Private type names shall use the following rule:

`t[Name]`

  - [Name]: type purpose description.

???
---

### Types: Private Types

```c
typedef struct
{
   U16 u16Command;
   U8  u8Data1;
   U8  u8Data2;
   U8 *pu8Result;
} tProtocolBuffer;
```

???
---

### Types: Public Types

Public type names shall use the following rule:

`[Lll][Mmm]_t[Name]`

  - [Lll]: architecture level
  - [Mmm]: module name
  - [Name]: descriptive name

???
---

### Types: Public Types

```c
typedef struct
{
   U16 u16Command;
   U8  u8Data1;
   U8  u8Data2;
   U8 *pu8Result;
} AppMdb_tProtocolBuffer;
```

???
---

### Types: Private enums

Private enum names shall use the following rule:

`e[Name]`

  - [Name]: descriptive name

???
---

### Types: Private enums

```c
typedef enum
{
   eStat1;
   eStat2;
   eStat3;
} tProtoStatus;
```

???
---

### Types: Public enums

Public enum names shall use the following rule:

`[Lll][Mmm]_e[Name]`

  - [Lll]: architecture level
  - [Mmm]: component name
  - [Name]: descriptive name

???
---

### Types: Public enums

```c
typedef enum
{
   eStat1;
   eStat2;
   eStat3;
} AppMdb_tProtoStatus;
```

???
---

### Variables: Private variables

Private variable names shall use the following rule:

`[p][size][Scope][Name]`

  - [p]: the variable is a pointer
  - [size]: size of the variable (u8, s16…)
  - [scope]: visibility and storage (g for file scope static variable, y for function scope static variable, z for a function scope variable)
  - [Name]: descriptive name

???
---

### Variables: Private variables

```c
static U8 u8gLocalVar;

static void LocalFunction ( void  )
{
   static U16 u16yStaticVar = 0 ;
}
```

???
---

### Variables: Public variables

Public variables names shall use the following rule:

`[Lll][Mmm]_[p][Name]`

  - [Lll]: architecture level
  - [Mmm]: component name
  - [p]: the variable is a pointer
  - [Name]: descriptive name

???
---

### Variables: Public variables

```c
U8 * HalSer_pUartPointer;
U8 HalSer_UartData;
```

???
---

### Constants: Private constants

Private constant names shall use the following rule:

`[p]c[size][Name]`

  - [p]: the constant is a pointer
  - [size]: size of the constant (u8, s16, ...)
  - [Name]: descriptive name

???
---

### Constants: Private constants

```c
static const U8 cu8RegisterDefault;
static const U8 *pcu8RegisterPointer;
```

???
---

### Constants: Public constants

Public constant names shall use the following rule:

`[Lll][Mmm]_[p]c[Name]`

  - [Lll]: architecture level
  - [Mmm]: component name
  - [p]: the constant is a pointer
  - [Name]: descriptive name

???
---

### Constants: Public constants

```c
const U8 *HalSer_pcu8RegisterPointer;
const U8 HalSer_cu8RsgisterValue;
```

???
---

### Defines: Private defines

Private defines names shall use the following rule:

`[NAME]`

  - [NAME]: descriptive name in upper case with _ division when applicable

???
---

### Defines: Private defines

```c
#define INIT_DISPLAY_LINES (7)
#define NUMBER_OF_POINTS (2)
```
???
---

### Defines: Public defines

Use the following rule:

`[LLL][MMM]_[NAME]`

  - [LLL]: architecture level
  - [MMM]: component name
  - [NAME]: descriptive name in upper case with _ division when applicable

???
---

### Defines: Public defines

```c
#define HALI2C_LOCAL_ADDRESS (0x06)
#define APPMDB_LOCAL_ADDRESS (0x44)
```

???
---

### Functions: Private functions

Use the following rule:

`[p][name][Action]`

  - [p]: the function returns a pointer type
  - [name][Action]: descriptive name including an action verb

???
---

### Functions: Private functions

```c
static void alarmSet( void  )
{
}

static U8 *palarmGet( void  )
{
}
```

???
---

### Functions: Public functions

Use the following rule:

`[Lll][Mmm]_[p][Name][Action]`

  - [Lll]: architecture level
  - [Mmm]: component name
  - [p]: the function returns a pointer type
  - [Name][Action]: descriptive name including an action verb

???
---

### Functions: Public functions

```c
void AppMen_Reset( void  )
{
}

U8 *AppMen_ppositionGet( void  )
{
}
```
???
---

layout: true
.footer[
Coding rules
]

???
---

## Coding rules

Developed software shall never break any mandatory
MISRA C 2004 rule and minimize breaking optional MISRA C 2004 rules.

???
---

### Coding rules: File contents

The content of a C source file shall be organized with:

  - File header
  - Includes for .h files 
  - Private Defines 
  - Private Types
  - Private variables
  - Public variables
  - Private functions prototypes
  - Private functions implementations
  - Public function implementations

???
---

### Coding rules: File contents

The content of a H source file shall be organized with:

  - File header
  - Mono inclusion start 
  - Includes for .h files
  - Public Defines  
  - Public Types
  - Public variables prototypes
  - Public functions prototypes
  - Mono inclusion end 

???
---

### Coding rules: Global Variables

The usage of global public variables shall be avoided.
Exchanging values between modules shall be performed
by architecture, with the aid of functions calls.

???
---

### Coding rules: Function Parameters

Function parameters shall always be tested before usage.
Implicit testing can be accepted.

### Coding rules: Functions return value

All functions shall have a unique return point (return keyword).

???
---

### Coding rules: Sources documentation 

All the sources shall be Doxygen compatible in their comments.
All functions shall have an Doxygen header with:

  - a brief description
  - parameter description
  - return value description

All the documentation shall be written inside C source files
and not inside H source files.

???
---

### Coding rules: Variables declaration

Each variable shall be declared in a separate line
and explicit inizialization shall be included while declaring.

A short description shall be included with declaration.

```c
U8 * HalSer_pRegisterPointer = NULL; /*!< Pointer to register location */

/*! UART register value */
static U8 gRegisterContent = 0;
```

???
---

### Coding rules: Indentation

Opening bracket is on the line following
the referring instruction at the same level,
following instructions are indented by 4 spaces.

```c
typedef enum
{
   eStat1;
   eStat2;
   eStat3;
} tProtoStatus;
```

???
---

### Coding rules: Conditions

The use of brackets is mandatory after all
conditional statements. The condition is always between parentheses.

For easy of reading a space after
and before each parenthesis shall be included.

???
---

### Coding rules: Conditions

```c
if ( bCondition == bEXIT )
{
   ...;
}

if ( cOutvalue == '\n' )
{
   ...;
}
```

???
---

### Coding rules: Conditions

When coding multiple conditions readability
of the condition shall be privileged.

???
---

### Coding rules: Conditions

```c
if ( ( bCondition == bEXIT ) && ( bVOutvlue == '\n' ) )
{
   ...;
}

if (    ( cOutValue == '\n' )
     || ( ( cOutValue != '\t' ) && ( cInValue != '\n' ) ) 
   )
{
   ...;
}
```

???
---

### Coding rules: Functions length

Function shall not exceed 80 lines.

A line shall not exceed 100 characters.

???
---

### Coding rules: Stop condition in loops

Stop condition in loops are never expressed with

```c
==
```

instead use

```c
<
<=
>
>=
```

???
---

### Coding rules: Magic numbers

It is forbidden to use magic numbers (constants expressed with digits
inside the sources).

Always use a const or a defined value.

???
---

### Coding rules: Parenthesis

A space character shall be inserted before and after each parenthesis,
bracket or embrace.

Never assume compiler sets proper operators priority.

???
---

### Coding rules: Parenthesis

```c
  a * b   / c + d;         /* wrong */
( a * b ) / ( c + d );     /* correct */
```

???
---

### Coding rules: Compilation warning 

Software shall build with zero warnings count,
zero errors count, in a condition where
the toolchain is configuder for the maximum attention level.
