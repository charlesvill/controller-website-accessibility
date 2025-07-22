diff --git a/src/components/pafr22visualise/bondsovertime.tsx b/src/components/pafr22visualise/bondsovertime.tsx
index d832434..1696323 100644
--- a/src/components/pafr22visualise/bondsovertime.tsx
+++ b/src/components/pafr22visualise/bondsovertime.tsx
@@ -68,6 +68,8 @@ export function BondsOverTime() {
         );
 
       const plotforbondsovertimeelem = Plot.plot({
+        ariaLabel: "Bonded debt and long term notes over time",
+        ariaDescription: "A grouped bar chart showing total bonded debt by fiscal year and activity type.",
         width: getWidthPlot(sizes),
         height: getHeightPlot(sizes),
         color: {
@@ -84,12 +86,14 @@ export function BondsOverTime() {
           Plot.lineY(bondeddebtandlongtermnotespayablecleanedtotals, {
             x: 'Fiscal Year',
             y: 'Total',
+            ariaHidden: true,
           }),
           Plot.textY(bondeddebtandlongtermnotespayablecleanedtotals, {
             x: 'Fiscal Year',
             y: 'Total',
             text: (bruh: any) => (bruh['Total'] / 10e8).toFixed(2),
             dy: -10,
+            ariaHidden: true,
           }),
           Plot.barY(bondeddebtandlongtermnotespayablecleaned, {
             x: 'Fiscal Year',
@@ -101,7 +105,7 @@ export function BondsOverTime() {
                 digits: 2,
               })}`,
           }),
-          Plot.ruleY([0]),
+          Plot.ruleY([0], { ariaHidden: true }),
         ],
       });
 
@@ -109,6 +113,7 @@ export function BondsOverTime() {
         console.log('current ref', bondsovertimeref.current);
         bondsovertimeref.current.innerHTML = '';
         bondsovertimeref.current.append(plotforbondsovertimeelem);
+        bondsovertimeref.current.setAttribute('role', 'img');
       }
     }
   };
@@ -136,10 +141,14 @@ export function BondsOverTime() {
     }
   }, []);
 
-  return <div 
-    ref={bondsovertimeref} 
-    id='bondschart4pafr'
-
-
-  ></div>;
+  return (
+    <figure>
+      <figcaption id="bondsovertime-caption">Bonds Over Time</figcaption>
+      <div
+        ref={bondsovertimeref}
+        id='bondschart4pafr'
+        aria-labelledby="bondsovertime-caption"
+      ></div>
+    </figure>
+  )
 }
diff --git a/src/pages/reports/pafr22.tsx b/src/pages/reports/pafr22.tsx
index fb2a2a9..6a7853f 100644
--- a/src/pages/reports/pafr22.tsx
+++ b/src/pages/reports/pafr22.tsx
@@ -732,4 +732,4 @@ export default function pafr22(props: any) {
       </Layout>
     </>
   );
-}
\ No newline at end of file
+}
