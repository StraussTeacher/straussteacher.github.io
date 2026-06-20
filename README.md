# straussteacher.github.io
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lernmodul: C# Vererbung im RPG-Szenario</title>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent-expert: #8e44ad;
            --bg-light: #f8f9fa;
            --text-dark: #333333;
            --border-color: #dddddd;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: var(--text-dark);
            background-color: #ffffff;
            margin: 0;
            padding: 0;
        }

        header {
            background-color: var(--primary);
            color: white;
            padding: 2rem 1rem;
            text-align: center;
        }

        .container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 2rem 1rem;
        }

        .grid-visuals {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1.5rem;
            margin: 2rem 0;
        }

        .card {
            background: var(--bg-light);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1.5rem;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        }

        .card.krieger { border-left: 5px solid #e74c3c; }
        .card.magier { border-left: 5px solid #3498db; }

        pre {
            background-color: #272822;
            color: #f8f8f2;
            padding: 1rem;
            border-radius: 5px;
            overflow-x: auto;
            font-family: 'Consolas', monospace;
            font-size: 0.9rem;
        }

        .keyword { color: #f92672; }
        .classname { color: #a6e22e; }

        /* Didaktische Boxen */
        .didactic-note {
            background-color: #e8f4f8;
            border-left: 5px solid var(--secondary);
            padding: 1rem;
            margin: 1.5rem 0;
            border-radius: 0 5px 5px 0;
        }

        /* Differenzierung nach oben */
        .expert-section {
            background-color: #faf5ff;
            border: 2px dashed var(--accent-expert);
            border-radius: 8px;
            padding: 2rem;
            margin-top: 4rem;
            position: relative;
        }

        .expert-badge {
            background-color: var(--accent-expert);
            color: white;
            padding: 0.25rem 0.75rem;
            font-size: 0.85rem;
            font-weight: bold;
            border-radius: 3px;
            position: absolute;
            top: -12px;
            left: 20px;
            text-transform: uppercase;
        }

        .self-check {
            background-color: #fcf8e3;
            border-left: 5px solid #f0ad4e;
            padding: 1rem;
            margin: 1.5rem 0;
        }

        footer {
            text-align: center;
            padding: 2rem;
            background-color: var(--bg-light);
            margin-top: 3rem;
            border-top: 1px solid var(--border-color);
        }
    </style>
</head>
<body>

    <header>
        <h1>C# Objektorientierung: Grundlagen der Vererbung</h1>
        <p>Didaktisch aufbereitetes Selbstlernmodul für Fachinformatiker</p>
    </header>

    <div class="container">
        
        <section id="intro">
            <h2>Der Einstieg: Vererbung verstehen</h2>
            <p>Vererbung dient der <strong>Strukturierung von Daten</strong> und der <strong>Vermeidung von redundantem Code (DRY - Don't Repeat Yourself)</strong>. Wir betrachten dies isoliert von der Polymorphie anhand eines Rollenspiels (RPG).</p>
            
            <div class="didactic-note">
                <strong>Didaktischer Hinweis (Logiklücken vermeiden):</strong> 
                Ein gutes Klassendesign bildet nur die Attribute ab, die für die jeweilige Rolle <em>essentiell</em> sind. Ein Krieger benötigt im Kampf mentale Fokussierung in Form von Wutpunkten. Ein Magier nutzt arkane Energie (Mana). Würden wir alle Attribute in eine einzige Riesen-Klasse stopfen, hätten wir Datenmüll (z.B. ungenutzte Mana-Felder beim Krieger).
            </div>
        </section>

        <section id="datenmodell">
            <h2>Das Klassenmodell im Code</h2>
            
            <h3>1. Die Basisklasse (Elternklasse)</h3>
            <p>Enthält Eigenschaften, die absolut jede Entität im Spiel besitzt.</p>
            <pre><code><span class="keyword">public class</span> <span class="classname">Spielfigur</span>
{
    <span class="keyword">public string</span> Name { <span class="keyword">get; set;</span> }
    <span class="keyword">public int</span> Lebenspunkte { <span class="keyword">get; set;</span> }

    <span class="keyword">public void</span> Bewegen()
    {
        Console.WriteLine(<span class="keyword">$"</span>{Name} bewegt sich.<span class="keyword">"</span>);
    }
}</code></pre>

            <h3>2. Die Spezialisierungen (Kindklassen)</h3>
            <p>Durch den Doppelpunkt <code>:</code> erben die Kindklassen alle Eigenschaften und Methoden der Basisklasse und erweitern diese.</p>
            
            <div class="grid-visuals">
                <div class="card krieger">
                    <h4>Der Krieger</h4>
                    <p><em>Erbt von Spielfigur.</em> Erhält exklusiv die Eigenschaft <code>Wutpunkte</code>. Er benötigt kein Mana, da seine Fähigkeiten auf physischer Kraft basieren.</p>
                    <pre><code><span class="keyword">public class</span> <span class="classname">Krieger</span> : <span class="classname">Spielfigur</span>
{
    <span class="keyword">public int</span> Wutpunkte { <span class="keyword">get; set;</span> }
}</code></pre>
                </div>
                
                <div class="card magier">
                    <h4>Der Magier</h4>
                    <p><em>Erbt von Spielfigur.</em> Erhält exklusiv die Eigenschaft <code>Mana</code>. Er trägt im System keine schwere Rüstung, weshalb dieses Attribut hier bewusst fehlt.</p>
                    <pre><code><span class="keyword">public class</span> <span class="classname">Magier</span> : <span class="classname">Spielfigur</span>
{
    <span class="keyword">public int</span> Mana { <span class="keyword">get; set;</span> }
}</code></pre>
                </div>
            </div>
        </section>

        <section id="praxis">
            <h2>Anwendungsbeispiel</h2>
            <p>Obwohl in der Klasse <code>Krieger</code> kein Name definiert wurde, können wir via Vererbung direkt darauf zugreifen:</p>
            <pre><code>Krieger krieger = <span class="keyword">new</span> Krieger();
krieger.Name = <span class="keyword">"Gimli"</span>;       <span class="comment">// Geerbt von Spielfigur</span>
krieger.Wutpunkte = 100;       <span class="comment">// Spezifisch für Krieger</span>
krieger.Bewegen();             <span class="comment">// Methode geerbt!</span></code></pre>
        </section>

        <section class="self-check">
            <h3>Selbstkontrolle (Differenzierung nach unten / Unterstützung)</h3>
            <p>Prüfe dein Wissen, bevor du weitergehst:</p>
            <ul>
                <li>Kann ein Magier-Objekt auf das Attribut <code>Wutpunkte</code> zugreifen? (Antwort: Nein, Geschwisterklassen teilen ihre spezifischen Attribute nicht).</li>
                <li>Welche Beziehung beschreibt die Vererbung? (Antwort: Eine "IS-A" / "IST-EIN"-Beziehung).</li>
            </ul>
        </section>

        <section class="expert-section">
            <span class="expert-badge">Erweiterung / Challenge (Nach oben)</span>
            <h2>Vertiefung: Das Diamond-Problem & C#-Besonderheiten</h2>
            <p><em>Hinweis: Bearbeite diesen Bereich erst, wenn du die obigen Grundlagen fehlerfrei verstanden hast!</em></p>
            
            <h3>Das Diamond-Problem (Mehrfachvererbung)</h3>
            <p>Stell dir vor, wir wollten eine Hybrid-Klasse namens <code>Kampfmagier</code> erstellen, die sowohl von <code>Krieger</code> als auch von <code>Magier</code> erbt. Das nennt man Mehrfachvererbung.</p>
            
            <p><strong>Das Problem:</strong> Angenommen, sowohl <code>Krieger</code> als auch <code>Magier</code> hätten eine Methode namens <code>Angreifen()</code> eigenständig implementiert. Wenn der <code>Kampfmagier</code> nun <code>Angreifen()</code> aufruft – welche Methode soll der Compiler wählen? Die des Kriegers oder die des Magiers? Diese fundamentale Mehrdeutigkeit nennt man das <strong>Diamond-Problem</strong> (Rauten-Problem).</p>
            
            <div class="didactic-note" style="border-color: var(--accent-expert); background-color: #f3e5f5;">
                <strong>Wie löst C# das?</strong>
                C# verbietet Mehrfachvererbung bei Klassen strikt! Eine Klasse kann nur <strong>eine</strong> Basisklasse haben. Wenn wir Schnittmengen erzwingen wollen, nutzen wir in C# <strong>Interfaces (Schnittstellen)</strong>, da eine Klasse beliebig viele Interfaces implementieren darf.
            </div>

            <h3>Weitere Profi-Keywords für C#</h3>
            <ul>
                <li><strong><code>base</code>-Keyword:</strong> Mit <code>base</code> kann die Kindklasse explizit auf Konstruktoren oder Member der Elternklasse zugreifen (z.B. bei der Konstruktor-Verkettung).</li>
                <li><strong><code>sealed</code>-Klassen:</strong> Wenn du verhindern willst, dass andere Entwickler von deiner Klasse erben können (z.B. aus Sicherheits- oder Performancegründen), markiere sie als <code>public sealed class AdminUser</code>. Die Vererbungslinie wird damit unwiderruflich abgeschnitten.</li>
            </ul>
        </section>

    </div>

    <footer>
        <p>Lernplattform für Fachinformatiker | Thema: OOP Vererbung in C#</p>
    </footer>

</body>
</html>
