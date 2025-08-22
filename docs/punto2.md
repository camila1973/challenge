---
layout: default
title: Punto2
nav_order: 2
---

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Construcción de Grafo</title>
        <style>
            body {
                font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
                margin: 0;
                padding: 20px;
                min-height: 100vh;
            }

            .container {
                max-width: 1200px;
                margin: 0 auto;
                background: rgba(255, 255, 255, 0.95);
                border-radius: 20px;
                padding: 30px;
                box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            }

            h1 {
                text-align: center;
                color: #2c3e50;
                margin-bottom: 30px;
                font-size: 2.5em;
                background: linear-gradient(45deg, #667eea, #764ba2);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
            }

            .step {
                margin: 30px 0;
                padding: 20px;
                border-radius: 15px;
                background: #f8f9fa;
                border-left: 5px solid #667eea;
                transition: all 0.3s ease;
            }

            .step:hover {
                transform: translateY(-2px);
                box-shadow: 0 10px 25px rgba(102, 126, 234, 0.2);
            }

            .step-title {
                font-size: 1.4em;
                font-weight: bold;
                color: #2c3e50;
                margin-bottom: 15px;
            }

            .input-section, .process-section {
                display: flex;
                justify-content: space-around;
                align-items: center;
                flex-wrap: wrap;
                gap: 20px;
                margin: 20px 0;
            }

            .edge-box {
                background: #e3f2fd;
                padding: 15px 20px;
                border-radius: 10px;
                border: 2px solid #2196f3;
                font-family: 'Courier New', monospace;
                font-weight: bold;
                color: #1565c0;
                box-shadow: 0 4px 8px rgba(33, 150, 243, 0.2);
            }

            .graph-container {
                display: flex;
                justify-content: space-around;
                margin: 20px 0;
                gap: 20px;
                flex-wrap: wrap;
            }

            .graph-section {
                background: white;
                padding: 20px;
                border-radius: 15px;
                border: 2px solid #ddd;
                min-width: 300px;
                box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            }

            .graph-title {
                font-weight: bold;
                color: #2c3e50;
                margin-bottom: 15px;
                font-size: 1.2em;
                text-align: center;
                background: linear-gradient(45deg, #667eea, #764ba2);
                -webkit-background-clip: text;
                -webkit-text-fill-color: transparent;
            }

            .adj-list {
                font-family: 'Courier New', monospace;
                line-height: 1.8;
                background: #f8f9fa;
                padding: 15px;
                border-radius: 10px;
            }

            .node {
                color: #e91e63;
                font-weight: bold;
            }

            .edge-detail {
                color: #4caf50;
                background: #e8f5e8;
                padding: 2px 6px;
                border-radius: 4px;
                margin: 0 2px;
            }

            .arrow {
                font-size: 2em;
                color: #667eea;
                animation: pulse 2s infinite;
            }

            @keyframes pulse {
                0%, 100% { transform: scale(1); }
                50% { transform: scale(1.1); }
            }

            .nodes-set {
                background: #fff3e0;
                border: 2px solid #ff9800;
                padding: 20px;
                border-radius: 15px;
                text-align: center;
                margin: 20px 0;
            }

            .final-result {
                background: linear-gradient(135deg, #4caf50, #8bc34a);
                color: white;
                padding: 25px;
                border-radius: 15px;
                text-align: center;
                margin: 30px 0;
                box-shadow: 0 10px 25px rgba(76, 175, 80, 0.3);
            }

            .code-box {
                background: #2d3748;
                color: #e2e8f0;
                padding: 15px;
                border-radius: 10px;
                font-family: 'Courier New', monospace;
                font-size: 0.9em;
                line-height: 1.5;
                margin: 15px 0;
                overflow-x: auto;
            }

            .keyword { color: #f56565; }
            .function { color: #68d391; }
            .string { color: #fbb6ce; }
            .comment { color: #a0aec0; }
        </style>
    </head>
    <body>
        <div class="container">
            <h1>🔗 Construcción de Grafo: build_graph()</h1>

            <div class="step">
                <div class="step-title">📝 1. Input: Lista de Aristas (Edges) - SOURCE = 0</div>
                <div class="input-section">
                    <div class="edge-box">(0, 1, 2)</div>
                    <div class="edge-box">(0, 2, 4)</div>
                    <div class="edge-box">(0, 4, -2)</div>
                    <div class="edge-box">(0, 5, 1)</div>
                    <div class="edge-box">(0, 6, 5)</div>
                    <div class="edge-box">(2, 3, 3)</div>
                    <div class="edge-box">(2, 4, 2)</div>
                    <div class="edge-box">(3, 8, -4)</div>
                    <div class="edge-box">(4, 3, 5)</div>
                    <div class="edge-box">(4, 8, 1)</div>
                    <div class="edge-box">(4, 7, 2)</div>
                    <div class="edge-box">(5, 7, -1)</div>
                    <div class="edge-box">(5, 8, -3)</div>
                    <div class="edge-box">(6, 7, 6)</div>
                    <div class="edge-box">(7, 8, 2)</div>
                </div>
                <p style="text-align: center; color: #666;">
                    Cada arista = (origen, destino, peso) | ⚠️ Algunos pesos son negativos
                </p>
            </div>

            <div class="arrow" style="text-align: center;">⬇️</div>

            <div class="step">
                <div class="step-title">🔄 2. Procesamiento: Para cada arista (u, v, w)</div>
                
                <div class="code-box">
    <span class="keyword">for</span> u, v, w <span class="keyword">in</span> edges:
        adj[u].<span class="function">append</span>((v, w))      <span class="comment"># Lista de salientes</span>
        radj[v].<span class="function">append</span>((u, w))     <span class="comment"># Lista de entrantes</span>
        nodes.<span class="function">add</span>(u); nodes.<span class="function">add</span>(v)  <span class="comment"># Colectar nodos</span>
                </div>
                
                <div class="process-section">
                    <div style="text-align: center;">
                        <h4>Procesando: (0, 1, 2)</h4>
                        <div style="background: #fff; padding: 15px; border-radius: 10px; border: 2px solid #2196f3;">
                            adj[0] ← (1, 2)<br>
                            radj[1] ← (0, 2)<br>
                            nodes ← {0, 1}
                        </div>
                    </div>
                </div>
            </div>

            <div class="arrow" style="text-align: center;">⬇️</div>

            <div class="step">
                <div class="step-title">📊 3. Resultado: Estructuras de Datos Construidas</div>
                
                <div class="graph-container">
                    <div class="graph-section">
                        <div class="graph-title">adj - Lista Salientes</div>
                        <div class="adj-list">
                            <span class="node">0:</span> [<span class="edge-detail">(1,2)</span>, <span class="edge-detail">(2,4)</span>, <span class="edge-detail">(4,-2)</span>, <span class="edge-detail">(5,1)</span>, <span class="edge-detail">(6,5)</span>]<br>
                            <span class="node">1:</span> []<br>
                            <span class="node">2:</span> [<span class="edge-detail">(3,3)</span>, <span class="edge-detail">(4,2)</span>]<br>
                            <span class="node">3:</span> [<span class="edge-detail">(8,-4)</span>]<br>
                            <span class="node">4:</span> [<span class="edge-detail">(3,5)</span>, <span class="edge-detail">(8,1)</span>, <span class="edge-detail">(7,2)</span>]<br>
                            <span class="node">5:</span> [<span class="edge-detail">(7,-1)</span>, <span class="edge-detail">(8,-3)</span>]<br>
                            <span class="node">6:</span> [<span class="edge-detail">(7,6)</span>]<br>
                            <span class="node">7:</span> [<span class="edge-detail">(8,2)</span>]<br>
                            <span class="node">8:</span> []
                        </div>
                    </div>
                    
                    <div class="graph-section">
                        <div class="graph-title">radj - Lista Entrantes</div>
                        <div class="adj-list">
                            <span class="node">0:</span> []<br>
                            <span class="node">1:</span> [<span class="edge-detail">(0,2)</span>]<br>
                            <span class="node">2:</span> [<span class="edge-detail">(0,4)</span>]<br>
                            <span class="node">3:</span> [<span class="edge-detail">(2,3)</span>, <span class="edge-detail">(4,5)</span>]<br>
                            <span class="node">4:</span> [<span class="edge-detail">(0,-2)</span>, <span class="edge-detail">(2,2)</span>]<br>
                            <span class="node">5:</span> [<span class="edge-detail">(0,1)</span>]<br>
                            <span class="node">6:</span> [<span class="edge-detail">(0,5)</span>]<br>
                            <span class="node">7:</span> [<span class="edge-detail">(4,2)</span>, <span class="edge-detail">(5,-1)</span>, <span class="edge-detail">(6,6)</span>]<br>
                            <span class="node">8:</span> [<span class="edge-detail">(3,-4)</span>, <span class="edge-detail">(4,1)</span>, <span class="edge-detail">(5,-3)</span>, <span class="edge-detail">(7,2)</span>]
                        </div>
                    </div>
                </div>
                
                <div class="nodes-set">
                    <h4>🎯 Conjunto de Nodos</h4>
                    <div style="font-family: 'Courier New', monospace; font-size: 1.2em;">
                        nodes = {0, 1, 2, 3, 4, 5, 6, 7, 8}
                    </div>
                    <p style="margin: 10px 0 0 0; color: #666; font-size: 0.9em;">
                        🏁 SOURCE = 0 (nodo inicial para algoritmos)
                    </p>
                </div>
            </div>

            <div class="arrow" style="text-align: center;">⬇️</div>

            <div class="final-result">
                <h3>🎉 Output Final</h3>
                <p style="font-size: 1.2em; margin: 0;">
                    <strong>return</strong> adj, radj, sorted(nodes)
                </p>
                <p style="margin: 10px 0 0 0; opacity: 0.9;">
                    ✓ Lista de adyacencia saliente<br>
                    ✓ Lista de adyacencia entrante<br>
                    ✓ Nodos ordenados
                </p>
            </div>

            <div style="background: #e8f4f8; padding: 20px; border-radius: 15px; border-left: 5px solid #2196f3; margin-top: 30px;">
                <h4 style="color: #1976d2; margin-top: 0;">💡 Análisis del Grafo Generado</h4>
                <div style="display: flex; gap: 20px; flex-wrap: wrap;">
                    <div style="flex: 1; min-width: 250px;">
                        <h5 style="color: #4caf50; margin-bottom: 10px;">✅ Características:</h5>
                        <ul style="color: #666; line-height: 1.8; margin: 0;">
                            <li><strong>9 nodos:</strong> 0, 1, 2, 3, 4, 5, 6, 7, 8</li>
                            <li><strong>15 aristas:</strong> Grafo denso</li>
                            <li><strong>Pesos negativos:</strong> -4, -3, -2, -1</li>
                            <li><strong>SOURCE = 0:</strong> Múltiples salidas</li>
                        </ul>
                    </div>
                    <div style="flex: 1; min-width: 250px;">
                        <h5 style="color: #f44336; margin-bottom: 10px;">⚠️ Casos especiales:</h5>
                        <ul style="color: #666; line-height: 1.8; margin: 0;">
                            <li><strong>Nodos sink:</strong> 1 y 8 (solo entradas)</li>
                            <li><strong>Nodo source:</strong> 0 (solo salidas)</li>
                            <li><strong>Hub nodo 8:</strong> 4 conexiones entrantes</li>
                            <li><strong>Peso mínimo:</strong> -4 en (3→8)</li>
                        </ul>
                    </div>
                </div>
                <div style="background: #fff3e0; margin-top: 15px; padding: 15px; border-radius: 10px;">
                    <strong>🚀 Ideal para:</strong> Algoritmos de camino más corto (Dijkstra, Bellman-Ford), análisis de flujo, detección de ciclos negativos
                </div>
            </div>
        </div>
    </body>
    </html>

    <style>
.embed-16x9{position:relative;padding-top:56.25%}
.embed-16x9 iframe{position:absolute;inset:0;width:100%;height:100%;border:0}
</style>

[Ver a pantalla completa]({{ '/slides/index.html' | relative_url }})