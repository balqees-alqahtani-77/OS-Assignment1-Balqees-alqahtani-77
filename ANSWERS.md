# Assignment Questions

## Instructions
Answer all 4 questions with detailed explanations. Each answer should be **3-5 sentences minimum** and demonstrate your understanding of the concepts.

---

## Question 1: Thread vs Process

**Question**: Explain the difference between a **thread** and a **process**. Why did we use threads in this assignment instead of creating separate processes?

**Your Answer:**

[الـ Process (العملية) هي برنامج قيد التشغيل ولها مساحة ذاكرة خاصة بها مستقلة تماماً عن العمليات الأخرى. كل عملية لها heap و stack خاصين. الـ Thread (الخيط) هو وحدة تنفيذ أصغر داخل العملية، والخيوط داخل نفس العملية تتشارك في نفس مساحة الذاكرة (heap) ولكن لكل خيط stack خاص به.

الفرق بينهم:

· الذاكرة: العمليات منفصلة عن بعض، الخيوط تتشارك الذاكرة
· كلفة الإنشاء: إنشاء عملية جديد ثقيل وبطيء، إنشاء خيط أخف وأسرع
· التواصل: العمليات تحتاج IPC (مثل pipes, sockets)، الخيوط تتواصل مباشرة عبر المتغيرات المشتركة

لماذا استخدمنا خيوط بدلاً من عمليات منفصلة في هذا الواجب؟

لأن محاكاة جدولة المعالج تحتاج إلى:

1. مشاركة البيانات بسرعة: في الكود حقنا، processMap يربط بين كل Thread و Process object - هذا سهل لأن الخيوط تتشارك الذاكرة
2. كلفة أقل: إنشاء 10-20 عملية منفصلة سيكون أبطأ بكثير من إنشاء خيوط
3. سهولة المزامنة: أسهل في إدارة الطابور (Queue) بين الخيوط

Reference from code: Thread thread = new Thread(process); هنا لفنا الـ Process داخل Thread عشان نستفيد من خفة الخيوط وسهولة التواصل.]

---

## Question 2: Ready Queue Behavior

**Question**: In Round-Robin scheduling, what happens when a process doesn't finish within its time quantum? Explain using an example from your program output.

**Your Answer:**

[في جدولة Round-Robin، إذا العملية ما خلصت خلال الوقت الكمي (time quantum)، تنقطع وتنعاد إدراجها في نهاية قائمة الانتظار (ready queue)، وتجي دورها مرة ثانية بعد ما كل العمليات الثانية تاخذ فرصتها.

Example from my output:

```
 ▶ P1 executing quantum [3000ms] 
 ⏸ P1 completed quantum 3000ms │ Overall progress: [████████░░░░░░░░░░░░] 40%
 Remaining time: 1500ms
 ↻ P1 yields CPU for context switch

┌─ Ready Queue ──────────────────────────────────────────────────────────────────
│ [P2 → P3 → P4 → P5 → P6 → P7 → P8 → P9 → P10 → P11 → P12 → P13 → P14 → P15 → P1]
└────────────────────────────────────────────────────────────────────────────────
```

Explanation of example: 
P1 كان له وقت كامل 4500ms، وخلص 3000ms فقط (أي 40% من إجمالي العملية). بقي له 1500ms. بدل ما يشتغل كامل الباقي، رجع لنهاية الطابور ورا P15 عشان العمليات الثانية تاخذ فرصتها. هذا يضمن العدالة (fairness) وما يسمح لأي عملية تمسك المعالج لفترة طويلة. في Round-Robin، كل العمليات تتعامل بنفس الطريقة بغض النظر عن أولويتها.

---]


---

## Question 3: Thread States

**Question**: A thread can be in different states: **New**, **Runnable**, **Running**, **Waiting**, **Terminated**. Walk through these states for one process (P1) from your simulation.

**Your Answer:**

[New: لما يتم إنشاء كائن الـ Thread باستخدام new Thread(process) لكن start() ما اننادى بعد. في الكود: Thread thread = new Thread(process);

Runnable: بعد استدعاء start()، الخيط يكون جاهز للتشغيل لكن ينتظر دوره من الـ scheduler. في الكود: currentThread.start(); ثم ينتظر في الطابور.

Running: لما الـ scheduler يختار الخيط ويبدأ بتنفيذ دالة run(). داخل Process.run()، الخيط يشغل الكود حق المحاكاة.

Waiting: أثناء تنفيذ Thread.sleep(runTime) داخل quantum، الخيط يدخل حالة انتظار مؤقت. في الكود: Thread.sleep(stepTime); - هنا الخيط ينتظر بدون ما يستهلك CPU.

Terminated: لما تخلص دالة run() بالكامل و remainingTime يوصل صفر. في الكود: بعد remainingTime = 0; وطباعة "finished execution!".

ملاحظة: P1 في محاكاتنا يرجع من Runnable إلى Running عدة مرات لأنه يشتغل ويوقف (preemptive) بسبب time quantum، وهذا هو جوهر Round-Robin scheduling.

---

---

## Question 4: Real-World Applications

**Question**: Give **TWO** real-world examples where Round-Robin scheduling with threads would be useful. Explain why this scheduling algorithm works well for those scenarios.

**Your Answer:**

### Example 1: Web Server (مثل Apache, Nginx)

Description: خادم الويب يستقبل آلاف الطلبات (requests) في الثانية من مستخدمين مختلفين. كل طلب يحتاج معالجة (قراءة ملف، استعلام قاعدة بيانات، إرجاع صفحة).

Why Round-Robin works well here:

· العدالة: كل طلب ياخذ وقت متساوي من المعالج، ما في طلب "يظلم" الثاني
· الاستجابة: المستخدمين ما ينتظرون طويل عشان خادم واحد يخلص كل الطلبات
· منع الجوع (Starvation): الطلبات القصيرة ما تتأخر ورا طلبات طويلة
· هذا اللي طبقناه بالضبط في الواجب: كل عملية (P1, P2, ...) تاخذ نفس الوقت الكمي

Example 2: Operating System Scheduler (نظام التشغيل نفسه)

Description: نظام التشغيل يدير عدة برامج مفتوحة في نفس الوقت (متصفح، وورد، سبوتيفاي، الخ). المعالج واحد لكن البرامج كثيرة.

Why Round-Robin works well here:

· المستخدم يحس إن كل البرامج تشتغل بنفس الوقت (time-sharing)
· استجابة سريعة: لما تكتب في وورد، تظهر الحروف فوراً حتى لو فيه برامج ثانية تشتغل
· توزيع عادل: برنامج ثقيل مثل تصدير فيديو ما يوقف باقي البرامج
· نفس اللي صار في واجبنا: المعالج (CPU) واحد لكنه يوزع الوقت بين العمليات بشكل متساوي
## Summary

Key concepts I understood through these questions:

1. Thread vs Process: أدركت أن الفرق الرئيسي بين الـ Process والـ Thread هو مشاركة الذاكرة. العمليات منفصلة تماماً عن بعضها، بينما الخيوط تتشارك في نفس مساحة الذاكرة وهذا يسهل التواصل بينها ويقلل كلفة الإنشاء. في الكود حقنا، هذا يفسر ليش استخدمنا processMap عشان نربط كل Thread مع Process object.
2. Round-Robin Scheduling: فهمت كيف يعمل نظام الجدولة الدائري بالتحديد. لما العملية ما تخلص خلال الوقت الكمي، ترجع لنهاية طابور الانتظار عشان كل العمليات تاخذ فرصة عادلة. هذا يمنع أي عملية من "السيطرة" على المعالج ويضمن استجابة النظام لجميع المهام.
3. Thread Lifecycle: تعلمت دورة حياة الخيط كاملة من New إلى Terminated. كل خيط يمر بمراحل: New (عند الإنشاء)، Runnable (بعد start())، Running (أثناء التنفيذ)، Waiting (خلال sleep())، وأخيراً Terminated (بعد الانتهاء). هذا الفهم ساعدني أتتبع الخيوط في الكود وأعرف وين بالضبط كل خيط موجود.

---

Concepts I need to study more:

1. Synchronization بين الخيوط: لاحظت في الكود أننا ما استخدمنا أي synchronized blocks أو locks. في تطبيقات حقيقية، لو عدة خيوط تعدل نفس البيانات، ممكن يصير مشاكل مثل race conditions. أحتاج أدرس كيف أحمي البيانات المشتركة بين الخيوط باستخدام synchronized و locks.
2. Deadlock Prevention: واجهت فكرة الـ deadlock في المحاضرات لكن ما طبقناها في هذا الواجب. لما يكون عندي خيوط متعددة تنتظر بعضها، ممكن النظام يتوقف كلياً. أحتاج أتعلم كيف أكتشف وأمنع deadlock في تطبيقات المستقبل.

---
