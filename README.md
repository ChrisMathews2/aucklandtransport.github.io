# aucklandtransport.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Auckland Council Complete Organizational Structure</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #0c1929 0%, #1a2942 50%, #0c1929 100%);
            color: #e0e0e0;
            min-height: 100vh;
            padding: 20px;
            overflow-x: auto;
        }

        .container {
            max-width: 1800px;
            margin: 0 auto;
            padding: 20px;
        }

        h1 {
            text-align: center;
            color: #64b5f6;
            margin-bottom: 30px;
            font-size: 2.2em;
            text-shadow: 0 0 20px rgba(100, 181, 246, 0.5);
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { text-shadow: 0 0 20px rgba(100, 181, 246, 0.5); }
            to { text-shadow: 0 0 30px rgba(100, 181, 246, 0.8), 0 0 40px rgba(100, 181, 246, 0.4); }
        }

        .org-chart {
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
        }

        .node {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            border-radius: 10px;
            padding: 12px 20px;
            margin: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            position: relative;
            min-width: 220px;
            text-align: center;
            border: 2px solid rgba(100, 181, 246, 0.3);
            font-size: 0.9em;
        }

        .node:hover {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 8px 20px rgba(100, 181, 246, 0.3);
            border-color: rgba(100, 181, 246, 0.6);
        }

        .node.governing-body {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            border-color: rgba(255, 107, 107, 0.5);
            font-size: 1.1em;
            min-width: 300px;
        }

        .node.ceo {
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            border-color: rgba(78, 205, 196, 0.5);
            font-size: 1.05em;
            min-width: 280px;
        }

        .node.director {
            background: linear-gradient(135deg, #2a5298 0%, #1e3c72 100%);
            min-width: 260px;
        }

        .node.maori {
            background: linear-gradient(135deg, #c94b4b 0%, #4b134f 100%);
            border-color: rgba(201, 75, 75, 0.5);
        }

        .node.cco {
            background: linear-gradient(135deg, #9c27b0 0%, #673ab7 100%);
            border-color: rgba(156, 39, 176, 0.5);
        }

        .node.local-board {
            background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%);
            border-color: rgba(255, 152, 0, 0.5);
            min-width: 160px;
            padding: 8px 12px;
            font-size: 0.85em;
        }

        .node.department {
            background: linear-gradient(135deg, #607d8b 0%, #455a64 100%);
            border-color: rgba(96, 125, 139, 0.5);
            font-size: 0.85em;
            min-width: 200px;
        }

        .node.sub-department {
            background: linear-gradient(135deg, #37474f 0%, #263238 100%);
            border-color: rgba(55, 71, 79, 0.5);
            font-size: 0.8em;
            min-width: 180px;
            padding: 8px 15px;
        }

        .node.committee {
            background: linear-gradient(135deg, #00897b 0%, #00695c 100%);
            border-color: rgba(0, 137, 123, 0.5);
            min-width: 240px;
        }

        .node.at-exec {
            background: linear-gradient(135deg, #7b1fa2 0%, #512da8 100%);
            border-color: rgba(123, 31, 162, 0.5);
            font-size: 0.85em;
        }

        .node-title {
            font-weight: bold;
            font-size: 0.95em;
            margin-bottom: 4px;
            color: #fff;
        }

        .node-name {
            color: #b3d9ff;
            font-size: 0.85em;
        }

        .node-details {
            font-size: 0.8em;
            color: #a0c4ff;
            margin-top: 4px;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease;
        }

        .node.expanded .node-details {
            max-height: 400px;
            margin-top: 8px;
        }

        .expand-indicator {
            position: absolute;
            right: 8px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 16px;
            transition: transform 0.3s ease;
        }

        .node.expanded .expand-indicator {
            transform: translateY(-50%) rotate(180deg);
        }

        .children {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 30px;
            position: relative;
            gap: 10px;
        }

        .children::before {
            content: '';
            position: absolute;
            top: -30px;
            left: 50%;
            width: 2px;
            height: 30px;
            background: linear-gradient(to bottom, transparent, #64b5f6);
            transform: translateX(-50%);
        }

        .child-group {
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
        }

        .child-group::before {
            content: '';
            position: absolute;
            top: -15px;
            left: 50%;
            width: 2px;
            height: 15px;
            background: #64b5f6;
            transform: translateX(-50%);
        }

        .sub-items {
            list-style: none;
            padding: 8px 0;
            margin: 0;
            display: none;
            text-align: left;
            font-size: 0.8em;
        }

        .node.expanded .sub-items {
            display: block;
        }

        .sub-items li {
            padding: 3px 0;
            color: #a0c4ff;
            transition: color 0.3s ease;
        }

        .sub-items li:hover {
            color: #fff;
        }

        .section-container {
            margin-top: 50px;
            width: 100%;
        }

        .section-title {
            color: #64b5f6;
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.3em;
            text-shadow: 0 0 10px rgba(100, 181, 246, 0.3);
        }

        .horizontal-group {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            margin-top: 15px;
        }

        .tier-three {
            background: linear-gradient(135deg, #303f9f 0%, #1976d2 100%);
            margin-top: 30px;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
            width: 100%;
        }

        .tier-three-items {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .tier-three-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 12px 20px;
            border-radius: 8px;
            flex: 1;
            min-width: 250px;
            transition: all 0.3s ease;
            border: 1px solid rgba(100, 181, 246, 0.3);
            cursor: pointer;
        }

        .tier-three-item:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateY(-3px);
            border-color: rgba(100, 181, 246, 0.6);
        }

        .departments-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 12px;
            margin-top: 15px;
        }

        .team-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-top: 20px;
        }

        @media (max-width: 768px) {
            .children {
                flex-direction: column;
                align-items: center;
            }
            
            .node {
                min-width: 200px;
                font-size: 0.8em;
            }

            h1 {
                font-size: 1.6em;
            }

            .horizontal-group {
                flex-direction: column;
                align-items: center;
            }
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% {
                box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            }
            50% {
                box-shadow: 0 4px 20px rgba(100, 181, 246, 0.4);
            }
            100% {
                box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            }
        }

        .advisory-panel {
            background: linear-gradient(135deg, #00796b 0%, #004d40 100%);
            border-color: rgba(0, 121, 107, 0.5);
            font-size: 0.8em;
            min-width: 160px;
            padding: 8px 12px;
        }

        .info-box {
            background: rgba(100, 181, 246, 0.1);
            border: 1px solid rgba(100, 181, 246, 0.3);
            border-radius: 8px;
            padding: 15px;
            margin: 20px 0;
            text-align: center;
            font-size: 0.85em;
            color: #a0c4ff;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Auckland Council Complete Organizational Structure</h1>
        
        <div class="info-box">
            Click on any box to expand and see more details • Last updated: January 2025
        </div>
        
        <div class="org-chart">
            <div class="node governing-body pulse" onclick="toggleNode(this)">
                <div class="node-title">Governing Body</div>
                <div class="node-name">Mayor Wayne Brown + 20 Councillors</div>
                <div class="node-details">Auckland's regional governing body making strategic decisions</div>
                <span class="expand-indicator">▼</span>
            </div>
            
            <div class="children">
                <div class="child-group">
                    <div class="node ceo" onclick="toggleNode(this)">
                        <div class="node-title">Chief Executive</div>
                        <div class="node-name">Phil Wilson</div>
                        <div class="node-details">CEO since 2024 • Former Director of Governance</div>
                        <ul class="sub-items">
                            <li>• Email: phil.wilson@aucklandcouncil.govt.nz</li>
                            <li>• Reports to Governing Body</li>
                            <li>• Leads 7,000+ staff</li>
                            <li>• Former Taituarā president</li>
                            <li>• Executive Officer: Kirstine Jones</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="children">
                        <div class="node director maori" onclick="toggleNode(this)">
                            <div class="node-title">Tumuaki Huanga Māori</div>
                            <div class="node-name">Nick Turoa</div>
                            <div class="node-details">Director Māori Outcomes • Leads Ngā Mātārae</div>
                            <ul class="sub-items">
                                <li><strong>Background:</strong></li>
                                <li>• Former DOC senior leader</li>
                                <li>• Te Ati Awa, Ngāti Raukawa whakapapa</li>
                                <li>• Treaty negotiator</li>
                                <li><strong>Key Units:</strong></li>
                                <li>• Māori Strategy Team</li>
                                <li>• Capability Building Unit</li>
                                <li>• Relationships Team</li>
                                <li>• Kia Ora Tāmaki Makaurau Framework</li>
                                <li>• Co-governance Support</li>
                                <li>  - Tūpuna Maunga Authority</li>
                                <li>  - Te Poari o Kaipatiki</li>
                                <li>  - Ngāti Whātua Ōrakei Reserves</li>
                            </ul>
                            <span class="expand-indicator">▼</span>
                        </div>
                        
                        <div class="node director" onclick="toggleNode(this)">
                            <div class="node-title">Director Group Strategy & CEO's Office</div>
                            <div class="node-name">Max Hardy</div>
                            <div class="node-details">Former Mayor's Chief of Staff • Ex-Meredith Connell Partner</div>
                            <ul class="sub-items">
                                <li><strong>Departments & Teams:</strong></li>
                                <li>• <strong>Group Strategy, Transformation & Partnerships</strong></li>
                                <li>  - Strategic Planning</li>
                                <li>  - Business Transformation</li>
                                <li>  - Partnership Development</li>
                                <li>• <strong>Sustainability Office</strong></li>
                                <li>  - Climate Action Team</li>
                                <li>  - Environmental Strategy</li>
                                <li>• <strong>Legal Services</strong></li>
                                <li>  - Corporate Legal</li>
                                <li>  - Property Legal</li>
                                <li>• <strong>Risk & Assurance</strong></li>
                                <li>  - Internal Audit</li>
                                <li>  - Risk Management</li>
                                <li>• <strong>People, Safety & Wellbeing</strong></li>
                                <li>  - HR Operations</li>
                                <li>  - Health & Safety</li>
                                <li>  - Organizational Development</li>
                                <li>• <strong>Communications & Marketing</strong></li>
                                <li>  - Media Relations</li>
                                <li>  - Digital Communications</li>
                                <li>  - Internal Communications</li>
                            </ul>
                            <span class="expand-indicator">▼</span>
                        </div>
                        
                        <div class="node director" onclick="toggleNode(this)">
                            <div class="node-title">Director Community</div>
                            <div class="node-name">Rachel Kelleher</div>
                            <div class="node-details">Former DOC & Waikato Regional Council • Duty Controller AEM</div>
                            <ul class="sub-items">
                                <li><strong>Departments:</strong></li>
                                <li>• <strong>Community Wellbeing</strong></li>
                                <li>  - Libraries (55 locations)</li>
                                <li>  - Community Development</li>
                                <li>  - Arts & Culture</li>
                                <li>• <strong>Pools & Leisure</strong></li>
                                <li>  - Aquatic Facilities</li>
                                <li>  - Leisure Centres</li>
                                <li>  - Recreation Programmes</li>
                                <li>• <strong>Parks & Community Facilities</strong></li>
                                <li>  - Regional Parks (28)</li>
                                <li>  - Local Parks</li>
                                <li>  - Community Centres</li>
                                <li>• <strong>Environmental Services</strong></li>
                                <li>  - Biodiversity Team</li>
                                <li>  - Pest Management</li>
                                <li>  - Environmental Monitoring</li>
                                <li>• <strong>Licensing & Compliance</strong></li>
                                <li>  - Animal Management</li>
                                <li>  - Alcohol Licensing</li>
                                <li>  - Food Safety</li>
                            </ul>
                            <span class="expand-indicator">▼</span>
                        </div>
                        
                        <div class="node director" onclick="toggleNode(this)">
                            <div class="node-title">Director Resilience & Infrastructure</div>
                            <div class="node-name">Barry Potter</div>
                            <div class="node-details">Civil Engineer • City Rail Link Sponsor Rep • Since 2015</div>
                            <ul class="sub-items">
                                <li><strong>Deputy Director: Parul Sood</strong></li>
                                <li>  - Former GM Waste Solutions</li>
                                <li>  - Chair, Waste Management Institute NZ</li>
                                <li><strong>Departments & Teams:</strong></li>
                                <li>• <strong>Auckland Emergency Management</strong></li>
                                <li>  - Emergency Operations Centre</li>
                                <li>  - Community Resilience</li>
                                <li>  - Disability Inclusion Programme</li>
                                <li>• <strong>Recovery Office (2023 Storms)</strong></li>
                                <li>  - Property Categorisation Team</li>
                                <li>  - Buy-out Programme</li>
                                <li>  - Navigation Service (15 staff)</li>
                                <li>• <strong>Healthy Waters & Flood Resilience</strong></li>
                                <li>  - Making Space for Water</li>
                                <li>  - Stormwater Operations</li>
                                <li>  - Flood Response Team</li>
                                <li>• <strong>Engineering & Technical Advisory</strong></li>
                                <li>  - Infrastructure Planning</li>
                                <li>  - Asset Management</li>
                                <li>• <strong>Building Consents</strong></li>
                                <li>  - Residential Consents</li>
                                <li>  - Commercial Consents</li>
                                <li>• <strong>Waste Solutions (GM: Parul Sood)</strong></li>
                                <li>  - Waste Collection</li>
                                <li>  - Resource Recovery</li>
                                <li>• <strong>City Centre Programmes</strong></li>
                            </ul>
                            <span class="expand-indicator">▼</span>
                        </div>
                        
                        <div class="node director" onclick="toggleNode(this)">
                            <div class="node-title">Group Chief Financial Officer</div>
                            <div class="node-name">Ross Tucker</div>
                            <div class="node-details">CPA Australia • Former Treasury Manager</div>
                            <ul class="sub-items">
                                <li><strong>Previous Role:</strong> Head of Financial Strategy 2018</li>
                                <li><strong>Departments:</strong></li>
                                <li>• <strong>Treasury</strong></li>
                                <li>  - Debt Management</li>
                                <li>  - Investment Management</li>
                                <li>  - Cash Management</li>
                                <li>• <strong>Rates & Valuations</strong></li>
                                <li>  - Rating Policy</li>
                                <li>  - Property Valuations</li>
                                <li>• <strong>Financial Strategy</strong></li>
                                <li>  - Long-term Planning</li>
                                <li>  - Budget Development</li>
                                <li>• <strong>Financial Advisory</strong></li>
                                <li>  - Business Partnering</li>
                                <li>  - Financial Analysis</li>
                                <li>• <strong>Infrastructure Funding</strong></li>
                                <li>  - Development Contributions</li>
                                <li>  - Special Funding Mechanisms</li>
                            </ul>
                            <span class="expand-indicator">▼</span>
                        </div>
                        
                        <div class="node director" onclick="toggleNode(this)">
                            <div class="node-title">Director Policy, Planning & Governance</div>
                            <div class="node-name">Megan Tyler</div>
                            <div class="node-details">25+ years experience • Trained Planner • Former Chief of Strategy</div>
                            <ul class="sub-items">
                                <li><strong>Career:</strong> Born & raised in Auckland</li>
                                <li><strong>Departments:</strong></li>
                                <li>• <strong>Public Policy</strong></li>
                                <li>  - Strategic Policy</li>
                                <li>  - Social Policy</li>
                                <li>  - Economic Policy</li>
                                <li>• <strong>Planning & Resource Consents</strong></li>
                                <li>  - District Planning</li>
                                <li>  - Resource Consents Processing</li>
                                <li>  - Unitary Plan Team</li>
                                <li>• <strong>Governance & Engagement</strong></li>
                                <li>  - Democratic Services</li>
                                <li>  - Local Board Support</li>
                                <li>  - Committee Support</li>
                                <li>  - Public Engagement</li>
                                <li>• <strong>Chief Economist Unit</strong></li>
                                <li>  - Economic Analysis</li>
                                <li>  - Data & Insights</li>
                                <li>• <strong>Infrastructure Funding Agreements</strong></li>
                            </ul>
                            <span class="expand-indicator">▼</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="tier-three">
                <h3 class="section-title">Tier-Three Functions (2024-25 CCO Integration)</h3>
                <div class="tier-three-items">
                    <div class="tier-three-item" onclick="toggleNode(this)">
                        <div class="node-title">Auckland Urban Development Office (AUDO)</div>
                        <div class="node-name">GM: Patrick Dougherty</div>
                        <div style="color: #a0c4ff; font-size: 0.85em; margin-top: 5px;">Former Kāinga Ora GM Construction</div>
                        <ul class="sub-items" style="display: none;">
                            <li><strong>Background:</strong></li>
                            <li>• 20+ years urban development</li>
                            <li>• MBIE Construction Panel Chair</li>
                            <li><strong>Teams:</strong></li>
                            <li>• Large Projects Team</li>
                            <li>• Strategic Growth Areas</li>
                            <li>• Developer Relations</li>
                            <li>• Urban Regeneration</li>
                            <li>• Priority Locations</li>
                            <li>• Crown & Iwi Partnerships</li>
                        </ul>
                    </div>
                    <div class="tier-three-item" onclick="toggleNode(this)">
                        <div class="node-title">Property Department</div>
                        <div class="node-name">GM: Ian Wheeler</div>
                        <div style="color: #a0c4ff; font-size: 0.85em; margin-top: 5px;">Former Eke Panuku COO</div>
                        <ul class="sub-items" style="display: none;">
                            <li><strong>Experience:</strong> 30 years property</li>
                            <li><strong>Previous:</strong> Housing NZ roles</li>
                            <li><strong>Teams:</strong></li>
                            <li>• Portfolio Management</li>
                            <li>• Marina Operations (3 marinas)</li>
                            <li>• Commercial Property</li>
                            <li>• Asset Optimisation</li>
                            <li>• Property Services</li>
                            <li>• Multi-billion $ portfolio</li>
                        </ul>
                    </div>
                    <div class="tier-three-item" onclick="toggleNode(this)">
                        <div class="node-title">Economic Development Office (EDO)</div>
                        <div class="node-name">GM: Pam Ford</div>
                        <div style="color: #a0c4ff; font-size: 0.85em; margin-top: 5px;">Former Tātaki Director • 99 staff</div>
                        <ul class="sub-items" style="display: none;">
                            <li><strong>Background:</strong></li>
                            <li>• Ex-NZTE senior roles</li>
                            <li>• Private sector experience</li>
                            <li><strong>Teams (99 staff):</strong></li>
                            <li>• 38 from Tātaki</li>
                            <li>• 57 from council programmes</li>
                            <li>• The Southern Initiative</li>
                            <li>• Local Economic Brokers</li>
                            <li>• Business Support Services</li>
                            <li>• Industry Development</li>
                        </ul>
                    </div>
                </div>
            </div>

            <div class="section-container">
                <h2 class="section-title">Key Committees of the Governing Body</h2>
                <div class="horizontal-group">
                    <div class="node committee" onclick="toggleNode(this)">
                        <div class="node-title">Transport, Resilience & Infrastructure</div>
                        <div class="node-name">Chair: Cr Andy Baker</div>
                        <ul class="sub-items">
                            <li>• Transport oversight</li>
                            <li>• Infrastructure planning</li>
                            <li>• Resilience & emergency mgmt</li>
                            <li>• Recovery programmes</li>
                            <li>• AT oversight</li>
                            <li>• Watercare liaison</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node committee" onclick="toggleNode(this)">
                        <div class="node-title">Planning, Environment & Parks</div>
                        <div class="node-name">Chair: Cr Richard Hills</div>
                        <ul class="sub-items">
                            <li>• Unitary Plan</li>
                            <li>• Environmental policy</li>
                            <li>• Parks strategy</li>
                            <li>• Climate action</li>
                            <li>• Resource management</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node committee" onclick="toggleNode(this)">
                        <div class="node-title">CCO Direction & Oversight</div>
                        <div class="node-name">Monitors CCO performance</div>
                        <ul class="sub-items">
                            <li>• CCO strategy alignment</li>
                            <li>• Performance monitoring</li>
                            <li>• Statement of Intent review</li>
                            <li>• CCO reform implementation</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node committee" onclick="toggleNode(this)">
                        <div class="node-title">Finance & Performance</div>
                        <div class="node-name">Budget & financial oversight</div>
                        <ul class="sub-items">
                            <li>• Annual budget</li>
                            <li>• Financial strategy</li>
                            <li>• Performance monitoring</li>
                            <li>• Rates setting</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node committee" onclick="toggleNode(this)">
                        <div class="node-title">Audit & Risk</div>
                        <div class="node-name">Risk & compliance</div>
                        <ul class="sub-items">
                            <li>• Internal audit</li>
                            <li>• Risk management</li>
                            <li>• Compliance monitoring</li>
                            <li>• External audit liaison</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>

                    <div class="node committee" onclick="toggleNode(this)">
                        <div class="node-title">Civil Defence & Emergency Mgmt</div>
                        <div class="node-name">Emergency preparedness</div>
                        <ul class="sub-items">
                            <li>• Emergency planning</li>
                            <li>• Response coordination</li>
                            <li>• Community resilience</li>
                            <li>• Recovery oversight</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                </div>
            </div>

            <div class="section-container">
                <h2 class="section-title">Council-Controlled Organisations (CCOs)</h2>
                <div class="horizontal-group">
                    <div class="node cco" onclick="toggleNode(this)">
                        <div class="node-title">Auckland Transport (AT)</div>
                        <div class="node-name">CEO: Dean Kimpton</div>
                        <div class="node-details">Board Chair: Richard Leggat</div>
                        <ul class="sub-items">
                            <li><strong>Status:</strong> Under legislative reform</li>
                            <li><strong>Budget:</strong> $1.7B annually</li>
                            <li><strong>Board:</strong> Cr Maurice Williamson</li>
                            <li><strong>Executive Team:</strong></li>
                            <li>• Murray Burt - Infrastructure & Place</li>
                            <li>• Stacey Van Der Putten - PT & Active Modes</li>
                            <li>• Simon Buxton - Customer & Network</li>
                            <li>• Scott Campbell - Strategy & Governance</li>
                            <li>• Dan Lambert - Partnerships</li>
                            <li>• Mark Laing - CFO</li>
                            <li>• Karen Duffy - People & Performance</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node cco" onclick="toggleNode(this)">
                        <div class="node-title">Watercare Services Ltd</div>
                        <div class="node-name">Limited liability company</div>
                        <div class="node-details">Commerce Commission oversight</div>
                        <ul class="sub-items">
                            <li><strong>Status:</strong> Outside reform scope</li>
                            <li><strong>Model:</strong> User-pays, no council funding</li>
                            <li><strong>Investment:</strong> $1.25B capital</li>
                            <li><strong>Operations:</strong> $850M annually</li>
                            <li><strong>Regulation:</strong> Charter until 2028</li>
                            <li><strong>Financial separation:</strong> July 2025</li>
                            <li><strong>Services:</strong></li>
                            <li>• Water supply</li>
                            <li>• Wastewater treatment</li>
                            <li>• Infrastructure maintenance</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node cco" onclick="toggleNode(this)">
                        <div class="node-title">Tātaki Auckland Unlimited</div>
                        <div class="node-name">Trust structure retained</div>
                        <div class="node-details">Partial integration complete</div>
                        <ul class="sub-items">
                            <li><strong>Remaining functions:</strong></li>
                            <li>• Auckland Zoo</li>
                            <li>• Auckland Art Gallery</li>
                            <li>• Museums</li>
                            <li>• Auckland Live venues</li>
                            <li>• Stadiums (Eden Park, Go Media)</li>
                            <li><strong>Transferred to council:</strong></li>
                            <li>• Economic development → EDO</li>
                            <li>• Major events → council</li>
                            <li>• Destination marketing → council</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    
                    <div class="node cco" onclick="toggleNode(this)">
                        <div class="node-title">Eke Panuku (Disestablished)</div>
                        <div class="node-name">Development Auckland</div>
                        <div class="node-details">Functions integrated into council</div>
                        <ul class="sub-items">
                            <li><strong>Status:</strong> Disestablished Dec 2024</li>
                            <li><strong>Functions transferred to:</strong></li>
                            <li>• Urban Development Office</li>
                            <li>• Property Department</li>
                            <li><strong>Former activities:</strong></li>
                            <li>• Urban regeneration</li>
                            <li>• Waterfront development</li>
                            <li>• Town centre renewal</li>
                            <li>• Property development</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>

                    <div class="node cco" onclick="toggleNode(this)">
                        <div class="node-title">Auckland Future Fund</div>
                        <div class="node-name">Investment vehicle</div>
                        <div class="node-details">Established 2024</div>
                        <ul class="sub-items">
                            <li><strong>Purpose:</strong> Long-term investment</li>
                            <li><strong>Status:</strong> Not in reform scope</li>
                            <li><strong>Focus:</strong></li>
                            <li>• Diversified investments</li>
                            <li>• Income generation</li>
                            <li>• Risk management</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>

                    <div class="node cco" onclick="toggleNode(this)">
                        <div class="node-title">Port of Auckland Ltd</div>
                        <div class="node-name">100% Council-owned</div>
                        <div class="node-details">Not technically a CCO</div>
                        <ul class="sub-items">
                            <li><strong>Value:</strong> $1.08B</li>
                            <li><strong>Operations:</strong> Container terminal</li>
                            <li><strong>Oversight:</strong> CCO Committee</li>
                            <li><strong>Focus areas:</strong></li>
                            <li>• Harbour health</li>
                            <li>• Māori outcomes</li>
                            <li>• Environmental plans</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                </div>
            </div>

            <div class="section-container">
                <h2 class="section-title">21 Local Boards</h2>
                <div class="horizontal-group">
                    <div class="node local-board">
                        <div class="node-title">Albert-Eden</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Devonport-Takapuna</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Franklin</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Great Barrier</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Henderson-Massey</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Hibiscus and Bays</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Howick</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Kaipātiki</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Māngere-Ōtāhuhu</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Manurewa</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Maungakiekie-Tāmaki</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Ōrākei</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Ōtara-Papatoetoe</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Papakura</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Puketāpapa</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Rodney</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Upper Harbour</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Waiheke</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Waitākere Ranges</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Waitematā</div>
                    </div>
                    <div class="node local-board">
                        <div class="node-title">Whau</div>
                    </div>
                </div>
            </div>

            <div class="section-container">
                <h2 class="section-title">Advisory Bodies & Panels</h2>
                <div class="horizontal-group">
                    <div class="node advisory-panel" onclick="toggleNode(this)">
                        <div class="node-title">Houkura</div>
                        <div class="node-name">Independent Māori Statutory Board</div>
                        <ul class="sub-items">
                            <li>• Treaty partnership</li>
                            <li>• Māori representation</li>
                            <li>• Committee appointments</li>
                            <li>• Independent of council</li>
                        </ul>
                        <span class="expand-indicator">▼</span>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Disability Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Youth Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Pacific Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Seniors Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Rainbow Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Ethnic Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Rural Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Heritage Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Business Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Climate Advisory Panel</div>
                    </div>
                    <div class="node advisory-panel">
                        <div class="node-title">Arts & Culture Advisory</div>
                    </div>
                </div>
            </div>

            <div class="section-container">
                <h2 class="section-title">Key Programmes & Initiatives</h2>
                <div class="departments-grid">
                    <div class="node sub-department">
                        <div class="node-title">City Rail Link</div>
                        <div class="node-name">$5.5B project</div>
                    </div>
                    <div class="node sub-department">
                        <div class="node-title">Making Space for Water</div>
                        <div class="node-name">Flood resilience</div>
                    </div>
                    <div class="node sub-department">
                        <div class="node-title">Recovery Office</div>
                        <div class="node-name">2023 weather events</div>
                    </div>
                    <div class="node sub-department">
                        <div class="node-title">Climate Action Plan</div>
                        <div class="node-name">Te Tāruke-ā-Tāwhiri</div>
                    </div>
                    <div class="node sub-department">
                        <div class="node-title">The Southern Initiative</div>
                        <div class="node-name">South Auckland focus</div>
                    </div>
                    <div class="node sub-department">
                        <div class="node-title">Safeswim Programme</div>
                        <div class="node-name">Water quality monitoring</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        function toggleNode(node) {
            node.classList.toggle('expanded');
            
            // Find sub-items if they exist
            const subItems = node.querySelector('.sub-items');
            if (subItems) {
                if (node.classList.contains('expanded')) {
                    subItems.style.display = 'block';
                } else {
                    subItems.style.display = 'none';
                }
            }
            
            // Add animation effect
            node.style.transform = 'scale(0.98)';
            setTimeout(() => {
                node.style.transform = '';
            }, 150);
        }

        // Add hover effects
        document.querySelectorAll('.node, .tier-three-item').forEach(node => {
            node.addEventListener('mouseenter', function() {
                this.classList.add('pulse');
            });
            
            node.addEventListener('mouseleave', function() {
                setTimeout(() => {
                    this.classList.remove('pulse');
                }, 1000);
            });
        });

        // Expand CEO and key nodes by default
        const ceoNode = document.querySelector('.node.ceo');
        if (ceoNode) {
            ceoNode.classList.add('expanded');
            const subItems = ceoNode.querySelector('.sub-items');
            if (subItems) subItems.style.display = 'block';
        }
    </script>
</body>
</html>
