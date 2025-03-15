# panda-lesson-2
panda 2

סיכום מפורט של דף ההסבר על pandas
1. התמרת נתונים ושינוי מבנה
pd.melt(df): ממיר עמודות לשורות (מקבץ מידע אנכי).
df.pivot(columns='var', values='val'): ממיר שורות לעמודות (מקבץ מידע אופקי).
2. שילוב ושרשור DataFrames
pd.concat([df1, df2]): מאחד DataFrames בשורות (הוספת שורות).
pd.concat([df1, df2], axis=1): מאחד DataFrames בעמודות (הוספת עמודות).
3. מיון, שינוי שמות וסידור
df.sort_values('mpg'): ממיין את השורות לפי עמודה (בסדר עולה).
df.sort_values('mpg', ascending=False): ממיין את השורות בסדר יורד.
df.rename(columns={'y': 'year'}): משנה את שמות העמודות.
df.sort_index(): ממיין את ה-DataFrame לפי האינדקס.
df.reset_index(): מאפס את האינדקס ומעביר את האינדקס לעמודה חדשה.
df.drop(columns=['Length', 'Height']): מוחק עמודות מסוימות.
4. יצירת DataFrame בדרכים שונות
קביעת נתונים לפי עמודות:
python
Copy
Edit
df = pd.DataFrame({"a": [4, 5, 6], "b": [7, 8, 9], "c": [10, 11, 12]}, index=[1, 2, 3])
קביעת נתונים לפי שורות:
python
Copy
Edit
df = pd.DataFrame([[4, 7, 10], [5, 8, 11], [6, 9, 12]], index=[1, 2, 3], columns=['a', 'b', 'c'])
יצירת DataFrame עם MultiIndex:
python
Copy
Edit
df = pd.DataFrame(
    {"a": [4, 5, 6], "b": [7, 8, 9], "c": [10, 11, 12]},
    index=pd.MultiIndex.from_tuples([('d', 1), ('d', 2), ('e', 2)], names=['n', 'v'])
)
5. חיבור שיטות בשרשרת (Method Chaining)
pandas מאפשר חיבור שיטות באופן קריא:
python
Copy
Edit
df = (pd.melt(df)
      .rename(columns={'variable': 'var', 'value': 'val'})
      .query('val >= 200'))
6. פעולות לוגיות ושאילתות
תנאים:
<, >, <=, >=, ==, != – השוואות לוגיות.
df.column.isin(values) – בדיקת חברות בקבוצה.
pd.isnull(obj), pd.notnull(obj) – בדיקת ערכים חסרים (NaN).
&, |, ~, ^ – אופרטורים לוגיים.
df.any(), df.all() – בדיקה האם יש ערכים אמתיים/כולם אמתיים.
7. שימוש בביטויים רגולריים (Regex)
'\.' – מתאמים למחרוזות שמכילות נקודה.
'Length$' – מתאמים למחרוזות שמסתיימות ב-"Length".
'^Sepal' – מתאמים למחרוזות שמתחילות ב-"Sepal".
'^x[1-5]$' – מתאמים למחרוזות שמתחילות ב-"x" ונגמרות ב-1,2,3,4,5.
'^(?!Species$).*' – מתאמים לכל המחרוזות חוץ מ-"Species".
8. בחירת נתונים וסינון
df[df.Length > 7] – בחירת שורות שעומדות בתנאי.
df.drop_duplicates() – הסרת שורות כפולות.
df.sample(frac=0.5) – דגימה רנדומלית של מחצית השורות.
df.head(n), df.tail(n) – בחירת n השורות הראשונות/האחרונות.
df[['width', 'length', 'species']] – בחירת עמודות מסוימות.
df.iloc[10:20] – בחירת שורות לפי אינדקס מספרי.
df.loc[:, 'x2':'x4'] – בחירת עמודות בטווח מסוים.
9. חיתוך נתונים וסוגי מיזוג (Joins)
pd.merge(adf, bdf, how='left', on='x1') – שמירת כל השורות מ-adf וצירוף ערכים מ-bdf.
pd.merge(adf, bdf, how='inner', on='x1') – שמירת רק השורות המשותפות.
pd.merge(adf, bdf, how='outer', on='x1') – שמירת כל הנתונים משני ה-DataFrames.
10. ניתוח נתונים וסטטיסטיקה
df.describe() – סיכום סטטיסטי לכל עמודה.
df['w'].value_counts() – ספירת מופעים של ערכים ייחודיים.
df['w'].nunique() – מספר הערכים הייחודיים.
df.mean(), df.median(), df.std(), df.var(), df.min(), df.max() – חישובי ממוצע, חציון, סטיית תקן וכו'.
11. יצירת עמודות חדשות
df.assign(Area=lambda df: df.Length * df.Height) – הוספת עמודה מחושבת.
df['Volume'] = df.Length * df.Height * df.Depth – הוספת עמודה רגילה.
12. פונקציות וקטוריות (Vector Functions)
df.shift(1) – הסטת נתונים בשורה אחת קדימה.
df.cumsum() – סכום מצטבר.
df.rank(method='min') – דירוג נתונים.
13. טיפול בערכים חסרים
df.dropna() – מחיקת שורות עם ערכים חסרים.
df.fillna(value) – מילוי ערכים חסרים בערך ספציפי.
14. עבודה עם קבוצות (GroupBy)
df.groupby(by="col") – קיבוץ לפי עמודה.
df.groupby(level="ind") – קיבוץ לפי אינדקס.
פונקציות קיבוץ: size(), agg(function), sum(), max(), min().
15. חלונות (Windows) ושימוש בגלגולים
df.expanding() – חישוב מצטבר.
df.rolling(n) – חישובים על חלונות של n ערכים.
16. הדמיה וגרפים
df.plot.hist() – יצירת היסטוגרמה.
df.plot.scatter(x='w', y='h') – יצירת תרשים פיזור.
סיכום כללי
מסמך זה מספק סקירה מלאה על השימושים הנפוצים בספריית pandas לעיבוד נתונים. הוא כולל:

תמרות נתונים – שינוי מבנה הנתונים.
שילוב ומיזוג – חיבור DataFrames בשורות ובעמודות.
מיון וסינון – בחירה, מיון וסינון שורות ועמודות.
ניתוח סטטיסטי – פונקציות סטטיסטיות ושימוש ב-GroupBy.
טיפול בערכים חסרים – הסרה או מילוי של NaN.
שימוש ב-Regex – התאמות מחרוזות על שמות עמודות.
שיטות מתקדמות – חישובים וקטוריים, חלונות וגרפים.
pandas היא ספרייה חזקה ביותר לעבודה עם נתונים, והתמצאות בפקודות הבסיסיות שלה מאפשרת עיבוד וניתוח נתונים ביעילות גבוהה. 🚀












