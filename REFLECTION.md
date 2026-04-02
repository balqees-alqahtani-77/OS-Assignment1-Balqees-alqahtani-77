# Reflection Questions

## Instructions
Answer the following questions about your learning experience. Each answer should be **at least 5-7 sentences** and show your understanding.

---

## Question 1: What did you learn about multithreading?

**Your Answer:**

[تعلمت من هذا الواجب كيف الخيوط (threads) تشتغل بشكل متزامن داخل برنامج واحد. أول شي، عرفت إن كل thread يمثل عملية مستقلة لكنها تشارك نفس الذاكرة مع الخيوط الثانية. ثاني شي، فهمت دورة حياة الخيط (New, Runnable, Running, Waiting, Terminated) وكيف تتحكم فيها باستخدام start() و join() و sleep(). اللي فاجأني هو كيف Round-Robin scheduler يوزع الوقت الكمي (time quantum) بين العمليات بشكل عادل، وكيف الخيط "يستسلم" (yield) CPU عشان غيره يشتغل. كمان تعلمت كيف أتتبع وقت الانتظار لكل عملية باستخدام System.currentTimeMillis().
]

---

## Question 2: What was the most challenging part of this assignment?

**Your Answer:**

[أصعب جزء كان حساب وقت الانتظار (waiting time) لكل عملية بشكل صحيح. المشكلة كانت لما العملية ترجع للطابور بعد ما تخلص جزئ من وقتها، كنت أحسب وقت الانتظار من أول مرة دخلت فيه الطابور مو من آخر مرة. هذا الخلل كان يسبب أرقام انتظار كبيرة جداً وغير منطقية. كمان التنسيق بين الملفين (Colors.java و SchedulerSimulation.java) كان تحدي لأن أي خطأ في استيراد الكلاسات يسبب أخطاء في الترجمة. الموضوع الثاني الصعب كان فهم متى أزيد عداد context switches بالتحديد.]

---

## Question 3: How did you overcome the challenges you faced?

**Your Answer:**

[استخدمت عدة طرق للتغلب على المشاكل. أولاً، استخدمت System.out.println() بشكل مكثف عشان أعرف وين الخلل بالضبط - كنت أطبع قيم lastReadyTime و currentTime قبل وبعد كل تحديث. ثانياً، رجعت لقراءة وثائق Java الرسمية لفهم كيف Thread.join() و Thread.sleep() تشتغل بالضبط. ثالثاً، قارنت الكود حقي مع الكود الأصلي عشان أشوف التعديلات اللي سويتها. كمان استخدمت Git commits عشان أرجع لنسخة سابقة إذا خربت شيء. أخيراً، طلبت مساعدة من زملائي في الجامعة وشرحت لهم المشكلة - أحياناً الشرح لشخص ثاني يوضح لك الحل بنفسك.]

---

## Question 4: How can you apply multithreading concepts in real-world applications?

**Your Answer:**

[في التطبيقات الواقعية، multithreading يستخدم بكثرة. مثلاً في متصفحات الويب (Chrome, Firefox): كل تبويب (tab) يشتغل في thread منفصل عشان لو تبويب واحد تعلق، ما يوقف المتصفح كامل. كمان تحميل الصور والفيديوهات يتم في خيوط خلفية عشان الواجهة تبقى سريعة. ثاني مثال: الألعاب الإلكترونية - لعبة مثل Minecraft أو Fortnite تستخدم thread منفصل للرسومات (graphics)، وآخر للصوت، وثالث لفيزياء اللعبة، ورابع للاتصال بالسيرفر. ثالث مثال: تطبيقات الجوال - لما تفتح تطبيق Instagram، التطبيق يحمل الصور والفيديوهات في خيوط خلفية عشان ما يوقف واجهة المستخدم. في هذا الواجب، طبقنا نفس المبدأ: كل عملية شغالة في thread خاص، وscheduler يديرها بشكل عادل. هذا المبدأ يسمى "responsive design" وهو أساسي في أي تطبيق حديث عشان المستخدم ما يحس بتأخير أو تعلق]

---

## Additional Reflections (Optional)

### What would you like to learn more about?

[Any topics related to threading, concurrency, or operating systems that you're curious about?]

---

### How confident do you feel about multithreading concepts now?

[Rate yourself and explain: Beginner / Intermediate / Confident]

[Explain your rating - what do you understand well? What needs more practice?]

---

### Feedback on the assignment

[Any comments about the assignment? Was it helpful? Too easy/hard? Suggestions for improvement?]
