# straussteacher.github.io

<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lernmodul: Vererbung in C#</title>
    <style>
        :root {
            --primary: #2b3e50;
            --secondary: #18bc9c;
            --dark: #2c3e50;
            --light: #f8f9fa;
            --warning: #e74c3c;
            --accent: #8e44ad;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            background-color: #f4f6f7;
            color: var(--dark);
            margin: 0;
            padding: 0;
        }

        header {
            background-color: var(--primary);
            color: white;
            padding: 2rem;
            text-align: center;
            border-bottom: 5px solid var(--secondary);
        }

        .container {
            max-width: 1100px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        .nav-modules {
            display: flex;
            gap: 1rem;
            margin-bottom: 2rem;
            justify-content: center;
        }

        .btn {
            padding: 0.75rem 1.5rem;
            background-color: var(--primary);
            color: white;
            text-decoration: none;
            border-radius: 5px;
            font-weight: bold;
            transition: background 0.3s;
        }

        .btn:hover {
            background-color: var(--secondary);
        }

        .btn-vertiefung {
            background-color: var(--accent);
        }

        .btn-vertiefung:hover {
            background-color: #732d91;
        }

        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            padding: 2rem;
            margin-bottom: 2rem;
            border-left: 5px solid var(--secondary);
        }

        .card-vertiefung {
            border-left: 5px solid var(--accent);
            background-color: #fdf6ff;
        }

        .badge {
            display: inline-block;
            padding: 0.25rem 0.5rem;
            background-color: var(--secondary);
            color: white;
            border-radius: 3px;
            font-size: 0.85rem;
            font-weight: bold;
            margin-bottom: 1rem;
        }

        .badge-danger {
            background-color: var(--warning);
        }

        .badge-vertiefung {
            background-color: var(--accent);
        }

        pre {
            background-color: #272822;
            color: #f8f8f2;
            padding: 1rem;
            border-radius: 5px;
            overflow-x: auto;
            font-family: 'Consolas', monospace;
        }

        .grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.5rem;
        }

        @media(min-width: 768px) {
            .grid {
                grid-template-columns: 1fr 1fr;
            }
        }

        .visual-placeholder {
            background-color: #e9ecef;
            border: 2px dashed #ced4da;
            border-radius: 5px;
            padding: 1rem;
            text-align: center;
            font-style: italic;
            color: #6c757d;
            margin: 1rem 0;
        }

        .alert-box {
            background-color: #fadbd8;
            border-left: 5px solid var(--warning);
            padding: 1rem;
            margin: 1rem 0;
            border-radius: 4px;
        }
    </style>
</head>
<body>

    <header>
        <h1>Objektorientierte Programmierung in C#</h1>
        <p>Didaktisches Selbstlernmedium: Das Prinzip der Vererbung</p>
    </header>

    <div class="container">
        
        <div class="nav-modules">
            <a href="#grundlagen" class="btn">Modul 1: Grundlagen</a>
            <a href="#vertiefung" class="btn btn-vertiefung">Modul 2: Vertiefung (Level Up!)</a>
        </div>

        <section id="grundlagen">
            <h2><span class="badge">Modul 1</span> Klassische Vererbung (Daten- & Strukturfokus)</h2>
            
            <div class="card">
                <h3>Das Szenario & Die Basisklasse</h3>
                <p>Wenn wir ein Rollenspiel (RPG) programmieren, teilen sich alle Entitäten Kern-Eigenschaften. Statt Code zu kopieren, nutzen wir eine <strong>Basisklasse</strong>.</p>
                
                <div class="visual-placeholder">
                    <strong>Grafik 1: Die Basisklasse</strong><br>
                    Ein zentraler Strukturkasten "Spielfigur" mit den Feldern [Name] und [Lebenspunkte]. Ein Pfeil zeigt nach unten zu den Spezialisierungen.
                </div>

                <pre><code>// Die übergeordnete Basisklasse
public class Spielfigur
{
    public string Name { get; set; }
    public int Lebenspunkte { get; set; }

    public void Bewegen()
    {
        Console.WriteLine($"{Name} bewegt sich vorwärts.");
    }
}</code></pre>
            </div>

            <div class="grid">
                <div class="card">
                    <h3>Abgeleitete Klasse: Der Krieger</h3>
                    <p>Ein Krieger <strong>ist eine</strong> Spielfigur. Er erbt Name und Lebenspunkte, benötigt aber eine eigene Ressource für Nahkampfangriffe: <strong>Wutpunkte</strong>.</p>
                    
                    <div class="visual-placeholder">
                        <strong>Grafik 2: Spezialisierung Krieger</strong><br>
                        Krieger-Icon in Plattenrüstung. Liste zeigt geerbte Variablen verblasst und die exklusive Variable [Wutpunkte] hervorgehoben.
                    </div>

                    <pre><code>// Syntax in C#: Doppelpunkt bedeutet "erbt von"
public class Krieger : Spielfigur
{
    public int Wutpunkte { get; set; }
}</code></pre>
                    <p><strong>Logik-Check (Differenzierung nach unten):</strong> Warum hat der Krieger kein Mana? Ein Krieger nutzt physische Kraft. Magische Energien würden das System unlogisch aufblähen.</p>
                </div>

                <div class="card">
                    <h3>Abgeleitete Klasse: Der Magier</h3>
                    <p>Ein Magier <strong>ist eine</strong> Spielfigur. Er benötigt für seine Zaubersprüche eine völlig andere Ressource als der Krieger: <strong>Mana</strong>.</p>
                    
                    <div class="visual-placeholder">
                        <strong>Grafik 3: Spezialisierung Magier</strong><br>
                        Magier-Icon mit Zauberstab. Zeigt die exklusive Variable [Mana] im Objekt-Speicher.
                    </div>

                    <pre><code>public class Magier : Spielfigur
{
    public int Mana { get; set; }
}</code></pre>
                    <p><strong>Logik-Check (Differenzierung nach unten):</strong> Warum trägt der Magier keine Rüstungswerte? Im Spieldesign verlässt er sich auf Schutzzauber und Stoffbekleidung. Schwere Rüstungswerte gehören strukturell nicht in diese Klasse.</p>
                </div>
            </div>

            <div class="card">
                <h3>Anwendung im Code</h3>
                <p>Objekte der abgeleiteten Klassen haben automatisch Zugriff auf die Eigenschaften der Basisklasse:</p>
                <pre><code>Krieger k = new Krieger();
k.Name = "Thorin";       // Geerbt aus Spielfigur!
k.Wutpunkte = 80;        // Direkt aus Krieger

Magier m = new Magier();
m.Name = "Gandalf";      // Geerbt aus Spielfigur!
m.Mana = 150;            // Direkt aus Magier</code></pre>
            </div>
        </section>

        <hr style="border: 2px solid var(--accent); margin: 4rem 0;">

        <section id="vertiefung">
            <h2><span class="badge badge-vertiefung">Modul 2</span> Vertiefung & Architektur-Herausforderungen</h2>
            
            <div class="alert-box">
                <strong>WICHTIGER HINWEIS:</strong> Dieses Modul dient als Differenzierung nach oben. Bearbeiten Sie diesen Abschnitt erst, wenn Sie Modul 1 vollständig verstanden und in der Praxis fehlerfrei angewendet haben!
            </div>

            <div class="card card-vertiefung">
                <h3>Das Diamond-Problem (Mehrfachvererbung)</h3>
                <p>In manchen Programmiersprachen (wie C++) kann eine Klasse von mehreren Klassen gleichzeitig erben. Das führt zu einem massiven logischen Konflikt, dem sogenannten <strong>Diamond-Problem (Smaragd- oder Diamant-Problem)</strong>.</p>
                
                <div class="visual-placeholder" style="border-color: var(--accent);">
                    <strong>Grafik 5: Das Diamond-Problem</strong><br>
                    Strukturbaum: [A] steht oben. [B] und [C] erben von [A]. Klasse [D] versucht, von [B] UND [C] gleichzeitig zu erben. Die Form bildet eine Raute (Diamant).
                </div>

                <h4>Das theoretische Dilemma im RPG:</h4>
                <ul>
                    <li>Angenommen, Klasse <code>B (Kampfmagier)</code> und Klasse <code>C (Paladin)</code> erben beide von <code>Spielfigur</code>.</li>
                    <li>Beide Klassen modifizieren intern die Art und Weise, wie Daten verwaltet werden (z.B. Speicher-Layouts).</li>
                    <li>Wenn nun eine neue Klasse <code>D (Magischer Ritter)</code> von <strong>B und C gleichzeitig</strong> erben würde, und man ruft eine geerbte Eigenschaft auf: Welche Version erhält Klasse D? Die von Klasse B oder Klasse C?</li>
                </ul>

                <p><strong>Die C#-Lösung:</strong> Um diese unlösbaren Mehrdeutigkeiten zu verhindern, erlaubt C# **keine Mehrfachvererbung für Klassen**. Jede Klasse hat exakt eine Elternklasse.</p>
            </div>

            <div class="card card-vertiefung">
                <h3>Wie löst man das in C#? (Schnittstellen/Interfaces)</h3>
                <p>Wenn ein Charakter zwingend Fähigkeiten aus zwei Welten braucht, greift man in C# auf <strong>Interfaces (Schnittstellen)</strong> zurück. Eine Klasse darf nur von einer Klasse erben, aber **unendlich viele Interfaces implementieren**.</p>
                
                <pre><code>// Ein Interface erzwingt nur die Struktur, es vererbt keine Variablen-Werte!
public interface IZauberbar
{
    int Mana { get; set; }
    void Zaubern();
}

// Der Kampfmagier erbt Basis-Daten vom Krieger UND implementiert das Magie-Interface
public class Kampfmagier : Krieger, IZauberbar
{
    public int Mana { get; set; }
    public void Zaubern() 
    {
        Console.WriteLine("Zauber gewirkt!");
    }
}</code></pre>
            </div>

            <div class="card card-vertiefung">
                <h3>Weiteres Expertenwissen: Das <code>sealed</code>-Keyword</h3>
                <p>Manchmal möchte man als Software-Architekt verhindern, dass andere Entwickler von einer Klasse erben (z.B. aus Sicherheitsgründen oder zur Performance-Optimierung).</p>
                <p>Mit dem Schlüsselwort <code>sealed</code> wird die Vererbungskette unwiderruflich gesperrt:</p>
                <pre><code>// Von dieser Klasse kann NIEMAND mehr erben
public sealed class Endboss : Spielfigur
{
    public int WeltuntergangsSchaden { get; set; }
}

// Das hier würde einen Compiler-Fehler erzeugen:
// public class MiniBoss : Endboss { } </code></pre>
            </div>
        </section>

    </div>

</body>
</html>
