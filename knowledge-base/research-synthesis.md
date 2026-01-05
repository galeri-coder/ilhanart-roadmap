<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --accent: #00ff88;
            --bg-app: #050505;
            --card-bg: rgba(255, 255, 255, 0.02);
            --border: rgba(0, 255, 136, 0.1);
        }
        
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body { 
            background: var(--bg-app); 
            color: #e0e0e0; 
            font-family: 'Inter', sans-serif; 
            padding: 50px 20px; 
            line-height: 1.6;
        }

        .archive-header { text-align: center; margin-bottom: 60px; }
        
        h1 { 
            font-family: 'JetBrains Mono'; 
            letter-spacing: 6px; 
            color: #fff; 
            font-size: 26px; 
            text-transform: uppercase;
            margin-bottom: 15px;
        }

        .subtitle { 
            color: var(--accent); 
            font-size: 10px; 
            font-family: 'JetBrains Mono'; 
            letter-spacing: 2px;
            text-transform: uppercase;
            opacity: 0.8;
        }

        .source-container { max-width: 900px; margin: 0 auto; }

        .source-card { 
            background: var(--card-bg); 
            border: 1px solid var(--border); 
            border-radius: 16px; 
            margin-bottom: 25px; 
            padding: 30px;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            backdrop-filter: blur(10px);
            position: relative;
        }

        .source-card:hover { 
            border-color: var(--accent); 
            background: rgba(0, 255, 136, 0.05);
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.6);
        }

        .ref-id { 
            font-family: 'JetBrains Mono'; 
            color: var(--accent); 
            font-size: 10px; 
            margin-bottom: 12px;
            opacity: 0.7;
            letter-spacing: 1px;
        }

        .ref-title { 
            font-weight: 600; 
            font-size: 18px; 
            color: #fff; 
            margin-bottom: 10px;
            letter-spacing: 0.5px;
        }

        .ref-author { 
            font-style: italic; 
            font-size: 13px; 
            color: #888; 
            margin-bottom: 20px;
            display: block;
        }

        .ref-summary { 
            font-size: 14px; 
            color: #bbb; 
            border-left: 2px solid var(--accent); 
            padding-left: 20px;
            font-weight: 300;
        }

        .impact-tag { 
            display: inline-block; 
            margin-top: 20px; 
            font-size: 10px; 
            background: rgba(0, 255, 136, 0.1); 
            color: var(--accent); 
            padding: 4px 12px; 
            border-radius: 20px;
            font-family: 'JetBrains Mono';
            border: 1px solid var(--border);
        }

        .footer-seal { 
            text-align: center; 
            margin-top: 80px; 
            font-family: 'JetBrains Mono'; 
            font-size: 9px; 
            color: #444; 
            letter-spacing: 3px;
            text-transform: uppercase;
        }
    </style>
</head>
<body>
    <div class="archive-header">
        <h1>Research Archive</h1>
        <div class="subtitle">Cognitive Logic & Attention Economics // [PoArt]</div>
    </div>

    <div class="source-container">
        <div class="source-card">
            <div class="ref-id">REF_ID: ZAKAY-BLOCK-1995</div>
            <div class="ref-title">The Attentional-Gate Model</div>
            <span class="ref-author">Zakay, D., & Block, R. A. (1995). Prospective and Retrospective Duration Judgments.</span>
            <div class="ref-summary">Foundational cognitive science explaining how our attention to time directly dictates its perceived passage. High focus slows down reality.</div>
            <div class="impact-tag">LOGIC: TIME DILATION</div>
        </div>

        <div class="source-card">
            <div class="ref-id">REF_ID: WARD-ET-AL-2017</div>
            <div class="ref-title">Brain Drain: The Smartphone Proximity Effect</div>
            <span class="ref-author">Ward, A. F., Duke, K., Gneezy, A., & Bos, M. W. (2017).</span>
            <div class="ref-summary">Research proving that the mere presence of digital noise reduces cognitive capacity, even when not in use.</div>
            <div class="impact-tag">LOGIC: NOISE FILTER</div>
        </div>

        <div class="source-card">
            <div class="ref-id">REF_ID: BARBER-ODEAN-2008</div>
            <div class="ref-title">The Individual Investor & Attention Mechanics</div>
            <span class="ref-author">Barber, B. M., & Odean, T. (2008). All That Glitters.</span>
            <div class="ref-summary">Analysis of how retail capital is irrationally driven by "Attention-Grabbing" events rather than fundamental architectural value.</div>
            <div class="impact-tag">LOGIC: ANTI-HYPE CORE</div>
        </div>

        <div class="source-card">
            <div class="ref-id">REF_ID: CARR-2010</div>
            <div class="ref-title">The Shallows: Digital Neurological Impact</div>
            <span class="ref-author">Carr, N. (2010). What the Internet Is Doing to Our Brains.</span>
            <div class="ref-summary">Evidence of how constant digital fragmentation destroys deep thinking and artistic long-form focus.</div>
            <div class="impact-tag">LOGIC: DEEP FOCUS PROTECTION</div>
        </div>
    </div>

    <div class="footer-seal">
        NOTARY_ID: ILHANART_GENESIS // ENCRYPTION: SHA-512 // STATUS: LOCKED
    </div>
</body>
</html>
