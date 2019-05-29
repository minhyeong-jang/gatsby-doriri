1.

<div id="brinza-task-description">
<p>You have an array of numbers and you would like to print these numbers in a tabular format to make them look more organized. Each cell of the table contains exactly one number and is surrounded by exactly four edges:</p>
<tt style="white-space:pre-wrap">+-+
|4|
+-+

+-----+
|12345|
+-----+</tt>

<p>As you can see above, each corner of the cell is represented by a "<tt style="white-space:pre-wrap">+</tt>" sign, vertical edges by "<tt style="white-space:pre-wrap">-</tt>" signs and horizontal edges by "<tt style="white-space:pre-wrap">|</tt>" signs. The width of the cell adjusts to accommodate the number of digits of the number written within it. There can be many cells in a row. Adjacent cells share an edge:</p>
<tt style="white-space:pre-wrap">+---+---+---+---+
|  4| 35| 80|123|
+---+---+---+---+</tt>
<p>Note that each cell has the same width. The width of the cell adjusts to match the width of the longest number in the table. The numbers in cells are aligned to the right, with any unused area in each cell filled with spaces.</p>
<p>The table can consist of many rows, and adjacent rows share an edge:</p>
<tt style="white-space:pre-wrap">+-----+-----+-----+-----+
|    4|   35|   80|  123|
+-----+-----+-----+-----+
|12345|   44|    8|    5|
+-----+-----+-----+-----+
|   24|    3|   22|   35|
+-----+-----+-----+-----+</tt>
<p>Your goal is to output a table containing all the numbers from a given array such that each row contains exactly K numbers. The last row can contain fewer numbers.</p>
<p>Write a function:</p>
<blockquote><p style="font-family: monospace; font-size: 9pt; display: block; white-space: pre-wrap"><tt>function solution(A, K);</tt></p></blockquote>
<p>that, given a non-empty array A consisting of N integers and an integer K, prints a string representing the formatted array. The numbers in the table should appear in the same order as the numbers in the array.</p>
<p>For example, given array A = [4, 35, 80, 123, 12345, 44, 8, 5] and K = 10, the resultant table will contain exactly one row, as shown below:</p>
<tt style="white-space:pre-wrap">+-----+-----+-----+-----+-----+-----+-----+-----+
|    4|   35|   80|  123|12345|   44|    8|    5|
+-----+-----+-----+-----+-----+-----+-----+-----+</tt>
<p>For A = [4, 35, 80, 123, 12345, 44, 8, 5, 24, 3], K = 4, the table would appear as follows:</p>
<tt style="white-space:pre-wrap">+-----+-----+-----+-----+
|    4|   35|   80|  123|
+-----+-----+-----+-----+
|12345|   44|    8|    5|
+-----+-----+-----+-----+
|   24|    3|
+-----+-----+</tt>
<p>Given A = [4, 35, 80, 123, 12345, 44, 8, 5, 24, 3, 22, 35] and K = 4, the table would appear as follows:</p>
<tt style="white-space:pre-wrap">+-----+-----+-----+-----+
|    4|   35|   80|  123|
+-----+-----+-----+-----+
|12345|   44|    8|    5|
+-----+-----+-----+-----+
|   24|    3|   22|   35|
+-----+-----+-----+-----+</tt>
<p>The function shouldn't return any value.</p>
<p>You can print a string to the output (without or with the end-of-line character) as follows:</p>
<blockquote><p style="font-family: monospace; font-size: 9pt; display: block; white-space: pre-wrap"><tt>process.stdout.write('sample string');
process.stdout.write('whole line\n');</tt></p></blockquote>
<p>Assume that:</p>
<blockquote><ul style="margin: 10px;padding: 0px;"><li>N is an integer within the range [<span class="number">1</span>..<span class="number">200</span>];</li>
<li>K is an integer within the range [<span class="number">1</span>..<span class="number">1,000,000,000</span>];</li>
<li>each element of array A is an integer within the range [<span class="number">0</span>..<span class="number">1,000,000,000</span>].</li>
</ul>
</blockquote><p>In your solution, focus on <b><b>correctness</b></b>. The performance of your solution will not be the focus of the assessment.</p>
</div>

```js
function pad(n, width) {
  n = n + ''
  return n.length >= width ? n : new Array(width - n.length + 1).join(' ') + n
}
const paintBorder = (repeatCount, borderLength) => {
  let border = '+'
  for (let i = 0; i < borderLength; i++) {
    border += `${'-'.repeat(repeatCount)}+`
  }
  return `${border}\n`
}
function solution(A, K) {
  const repeatCount = Math.max.apply(null, A).toString().length
  let count = 0
  let answer = paintBorder(repeatCount, A.length > K ? K : A.length)
  for (let i = 0; i < A.length; i++) {
    if (i && i % K === 0) {
      answer += `|\n${paintBorder(repeatCount, count)}`
      count = 0
    }
    answer += `|${pad(A[i] ? A[i] : '', repeatCount)}`
    count++
  }
  answer += `|\n${paintBorder(repeatCount, count)}`
  console.log(answer.trim())
}

solution([4, 35, 80, 123, 12345, 44, 8, 5], 10)
solution([4, 35, 80, 123, 12345, 44, 8, 5, 24, 3], 4)
solution([4, 35, 80, 123, 12345, 44, 8, 5, 24, 3, 22, 35], 4)
```

<div id="brinza-task-description">
<p>You are in a browser-like environment, where you have access to the window object, the document object, and also $ − the jQuery library. The document contains a two-dimensional table. Each cell of the table has an upper-case letter in it and has its background color and text color set. Your task is simply to read the letters in row-major order (top to bottom, left to right), concatenate them into a single string and return it. However, you need to skip the letters that cannot be seen by the human eye. These are the ones whose colour is exactly the same as their background (that is, even marginal difference can be distinguished by a human eye).</p>
<p>The table is created using "<tt style="white-space:pre-wrap">table</tt>", "<tt style="white-space:pre-wrap">tbody</tt>", "<tt style="white-space:pre-wrap">tr</tt>" and "<tt style="white-space:pre-wrap">td</tt>" tags. Each "<tt style="white-space:pre-wrap">td</tt>" tag has a "<tt style="white-space:pre-wrap">style</tt>" attribute with its CSS "<tt style="white-space:pre-wrap">background-color</tt>" and "<tt style="white-space:pre-wrap">color</tt>" attributes set. There is the same number of cells in each row.</p>
<p>Write a function</p>
<tt style="white-space:pre-wrap">    function solution();</tt>
<p>that, given a DOM tree representing an HTML document, returns a string containing all visible letters, read in row-major order.</p>
<p>For example, given a document which has the following table in its body:</p>
<tt style="white-space:pre-wrap">    &lt;table&gt;
        &lt;tbody&gt;
        &lt;tr&gt;
            &lt;td style="color: #ff00ff; background-color:#FFFFFF"&gt;Q&lt;/TD&gt;
            &lt;td style="background-color: #442244; color: #442244"&gt;Y&lt;/td&gt;
            &lt;td style="color: #FFFF00; background-color:#442244"&gt;A&lt;/td&gt;
        &lt;/tr&gt;
        &lt;tr&gt;
            &lt;td style="color: #FFEEFE; background-color:#990000"&gt;Q&lt;/td&gt;
            &lt;td style="color: #FFFF00; background-color:#FF0"&gt;M&lt;/td&gt;
            &lt;td style="color: #000000; background-color:#FF7777"&gt;O&lt;/td&gt;
        &lt;/tr&gt;
        &lt;/tbody&gt;
    &lt;/table&gt;</tt>
<p>which, when displayed in a browser, produces the following output:</p>
    <table style="margin: 0 auto">
        <tbody>
        <tr>
            <td style="color: #ff00ff; background-color:#FFFFFF">Q</td>
            <td style="background-color: #442244; color: #442244">Y</td>
            <td style="color: #FFFF00; background-color:#442244">A</td>
        </tr>
        <tr>
            <td style="color: #FFEEFE; background-color:#990000">Q</td>
            <td style="color: #FFFF00; background-color:#FF0">M</td>
            <td style="color: #000000; background-color:#FF7777">O</td>
        </tr>
        </tbody>
    </table><p>your function should return "<tt style="white-space:pre-wrap">QAQO</tt>", since the letters "<tt style="white-space:pre-wrap">Y</tt>" and "<tt style="white-space:pre-wrap">M</tt>" are invisible.</p>
<p>Assume that:</p>
<blockquote><ul style="margin: 10px;padding: 0px;"><li>the DOM tree represents a valid HTML5 document;</li>
<li>there is exactly one table in the document, it has at least one cell and every row has the same number of cells;</li>
<li>the only child of <tt style="white-space:pre-wrap">&lt;body&gt;</tt> is <tt style="white-space:pre-wrap">&lt;table&gt;</tt>;</li>
<li>the length of the HTML document does not exceed 4KB;</li>
<li>jQuery 2.1 is supported;</li>
<li>all colors are provided as hex codes;</li>
<li>each pair of distinct colors occuring on input can be distinguished by a human eye (for example <tt style="white-space:pre-wrap">#000000</tt> is different than <tt style="white-space:pre-wrap">#000001</tt>).</li>
</ul>
</blockquote><p>In your solution, focus on <b><b>correctness</b></b>. The performance of your solution will not be the focus of the assessment.</p>
</div>

```js
/**
 * table의 td element를 불러옵니다.
 * 가져온 td element를 반복하며 backgroundColor, color 이 동일한지 비교합니다.
 * 동일한 경우 td 내 text를 return합니다.
 * return 된 요소를 배열로 만들고 join 합니다.
 */

function solution() {
  return $('table tbody tr td')
    .map((index, element) => {
      const ele = $(element)
      if (ele.css('background-color') !== ele.css('color')) return ele.text()
    })
    .get()
    .join('')
}
```

<div id="brinza-task-description">
<p>You are given a DOM tree and have to analyze the <tt style="white-space:pre-wrap">&lt;ul&gt;</tt> and <tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list tags within it. Your task is to find the maximum depth of nested <tt style="white-space:pre-wrap">&lt;ul&gt;</tt>/<tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list tags. A single <tt style="white-space:pre-wrap">&lt;ul&gt;</tt>/<tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list is nested one level deep. Each <tt style="white-space:pre-wrap">&lt;ul&gt;</tt>/<tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list inside another <tt style="white-space:pre-wrap">&lt;ul&gt;</tt>/<tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list is nested one level deeper. If there are no <tt style="white-space:pre-wrap">&lt;ul&gt;</tt> or <tt style="white-space:pre-wrap">&lt;ol&gt;</tt> lists at all in the DOM tree, the depth of nesting is 0.</p>
<p>Note that <tt style="white-space:pre-wrap">&lt;ul&gt;</tt>/<tt style="white-space:pre-wrap">&lt;ol&gt;</tt> lists can be nested directly or indirectly; that is, a <tt style="white-space:pre-wrap">&lt;ul&gt;</tt> list inside a table inside an <tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list is nested two levels deep.</p>
<p>For example, given an HTML document with the following contents within the <tt style="white-space:pre-wrap">&lt;body&gt;</tt> tag:</p>
<tt style="white-space:pre-wrap">&lt;ul&gt;
  &lt;li&gt;Item:
     &lt;ol&gt;
       &lt;li&gt;Point:
         &lt;div&gt;
           &lt;ul&gt;
             &lt;li&gt;elem1&lt;/li&gt;
           &lt;/ul&gt;
         &lt;/div&gt;
       &lt;/li&gt;
     &lt;/ol&gt;
  &lt;/li&gt;
  &lt;li&gt;elem2&lt;/li&gt;
&lt;/ul&gt;
&lt;ul&gt;
  &lt;li&gt;simple list1&lt;/li&gt;
&lt;/ul&gt;
&lt;ul&gt;
&lt;/ul&gt;</tt>
<p>there is a <tt style="white-space:pre-wrap">&lt;ul&gt;</tt> list nested three levels deep. Namely, "<tt style="white-space:pre-wrap">elem1</tt>" is in a <tt style="white-space:pre-wrap">&lt;ul&gt;</tt> list which is inside an <tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list containing "<tt style="white-space:pre-wrap">Point</tt>", while this <tt style="white-space:pre-wrap">&lt;ol&gt;</tt> list is inside another <tt style="white-space:pre-wrap">&lt;ul&gt;</tt> list containing "<tt style="white-space:pre-wrap">Item</tt>".</p>
<p>Write a function:</p>
<tt style="white-space:pre-wrap">    function solution();</tt>
<p>that, given a DOM tree, returns the maximum depth of nested <tt style="white-space:pre-wrap">&lt;ul&gt;</tt>/<tt style="white-space:pre-wrap">&lt;ol&gt;</tt> lists. For example, given the DOM tree of the document shown above, the function should return 3, as explained above.</p>
<p>Given the following content:</p>
<tt style="white-space:pre-wrap">&lt;ol&gt;
  &lt;li&gt;
    &lt;ol&gt;
      &lt;li&gt;&lt;/li&gt;
    &lt;/ol&gt;
  &lt;/li&gt;
&lt;/ol&gt;</tt>
<p>the function should return 2.</p>
<p>Assume that:</p>
<blockquote><ul style="margin: 10px;padding: 0px;"><li>the DOM tree represents a valid HTML5 document;</li>
<li>length of the HTML document does not exceed 4KB;</li>
<li>jQuery 2.1 is supported.</li>
</ul>
</blockquote></div>

```js
/**
 * ul, ol 리스트를 불러 온 후, 각 ul, ol의 depth를 조회합니다.
 * depth가 저장된 depthList 에서 최대값을 return 합니다.
 *
 * ul, ol 태그가 없는 경우 0을 return 하도록 설정합니다.
 */

function solution() {
  const depthList = $('ul, ol').map((index, ele) => {
    return $(ele).parents('ul, ol').length + 1
  })
  return depthList.length !== 0 ? Math.max.apply(null, depthList) : 0
}
```
