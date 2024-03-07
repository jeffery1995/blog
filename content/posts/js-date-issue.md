---
title: "EcmaScript 新特性 - Temporal API"
author: "Jeffery Jiang"
summary: "JavaScript Temporal API：新时代的日期和时间处理"
tags: ["javascript"]
date: "2022-11-09"
---

- [前言](#前言)
- [现有的Date API存在的缺陷](#现有的date-api存在的缺陷)
- [主要功能和优势](#主要功能和优势)
- [支持情况](#支持情况)


### 前言

随着时间在现代软件开发中的重要性日益增长，处理日期和时间的复杂性也变得越来越明显。传统的 JavaScript Date API 虽然功能强大，但也存在一些限制和缺陷，导致开发者不得不依赖于第三方库或手动编写复杂的代码来处理日期和时间。

为了解决这些问题，JavaScript Temporal API 应运而生。这是一个全新的日期和时间处理 API，旨在提供更简洁、更直观和更安全的方式来处理日期和时间。它提供了一组全新的对象和函数，可以轻松地执行各种日期和时间操作，同时解决了传统 Date API 中存在的一些问题。

### 现有的Date API存在的缺陷

现在的Date API 设计于20几年前，而且是参照当时的Java版本。其具体的缺陷主要包括以下几点：

- **月份，星期索引从0开始**：在 Date API 中，月份的索引是从0开始的，这与人们通常的习惯不符，容易引起误解和错误。例如，new Date(2024, 2, 7) 创建的是 2024 年 3 月 7 日，而不是 2 月 7 日。

- **时区处理不直观**：Date API 中对时区的处理相对复杂且不直观，开发者经常需要手动进行时区转换，这容易引发错误。例如，在不同的时区下，同一时间点可能会被解释为不同的日期时间。

- **可变性**：Date 对象是可变的，这意味着可以修改已经创建的日期，而不会触发任何警告或错误。这可能导致不可预料的行为，特别是在多线程或异步环境下。

- **有限的日期范围**：Date API 对日期的表示范围有限，只能表示从1970年1月1日到2100年之间的日期，这限制了其在一些应用场景下的使用。

下面是一些示例代码，说明了传统的 JavaScript Date API 的一些缺陷

```javascript
// 月份索引从0开始，容易引起误解
const date = new Date(2024, 2, 7); // 表示的是2024年3月7日，而不是2月7日

// 星期也是从0开始索引
const birthday = new Date('August 19, 1975 23:15:30');
const day1 = birthday.getDay(); // Sunday - Saturday : 0 - 6

// 时区处理不直观，需要手动进行时区转换
const dateUTC = new Date(Date.UTC(2024, 2, 7)); // 表示的是UTC时间，需要手动进行时区转换

// Date 对象可变性，容易导致不可预料的行为
const now = new Date();
now.setDate(now.getDate() + 7); // 修改了原始日期对象，可能导致意外的结果

// 有限的日期范围
const futureDate = new Date(3000, 0, 1); // 无法表示3000年以后的日期

```

这些缺陷使得传统的 Date API 在处理日期和时间时显得笨拙和容易出错，因此 JavaScript Temporal API 的推出填补了这些空白，提供了一种更现代、更安全和更直观的方式来处理日期和时间数据。

### 主要功能和优势

JavaScript Temporal API 的主要功能和优势包括：

- **更丰富的对象类型**：Temporal API 提供了一系列新的对象类型，如 Temporal.Instant、Temporal.Duration、Temporal.TimeZone 等，这些对象更加贴合现实世界中的概念，使开发者能够更轻松地处理日期和时间数据。

- **不可变性**：与传统的 Date 对象不同，Temporal API 中的对象都是不可变的。这意味着一旦创建了一个对象，就无法修改它的值，这有助于减少由于日期和时间变化而引起的错误。

- **严格的类型检查**：Temporal API 引入了严格的类型检查，确保开发者在处理日期和时间时不会出现意外的类型错误，从而提高了代码的可靠性和稳定性。

- **更简洁的 API 设计**：Temporal API 的设计更加简洁和直观，使开发者能够更轻松地执行各种日期和时间操作，而无需编写复杂的代码。

以下是一些使用 JavaScript Temporal API 的示例代码：

```javascript
// 创建一个表示当前时间的 Temporal.Instant 对象
const now = Temporal.now.instant();

// 创建一个表示明天这个时间点的 Temporal.Instant 对象
const tomorrow = now.plus({ days: 1 });

// 计算两个时间点之间的时间间隔
const difference = tomorrow.since(now);

// 输出时间间隔的天数
console.log(`明天距离现在 ${difference.total({unit: 'days'})} 天`);
```

### 支持情况

截至目前，JavaScript Temporal API 还在 [tc39的 stage 3阶段](https://github.com/tc39/proposal-temporal)，所以浏览器支持情况并[不是很完善](https://caniuse.com/temporal)。目前，Chrome 和 Firefox 浏览器已经支持了部分功能，而其他浏览器则需要借助 polyfill 或者额外的库来实现相同的功能。不过随着时间的推移，我们可以期待更多浏览器对 Temporal API 的支持会越来越完善。 当然，现在有一些第三方library也提供了比较完善的日期处理功能，比如`moment.js` 和`day.js`。



