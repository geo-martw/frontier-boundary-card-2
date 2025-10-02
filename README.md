<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Frontier Boundary Card #2: Data Access Boundary</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            padding: 20px;
            line-height: 1.6;
        }
        
        .card {
            max-width: 900px;
            margin: 0 auto;
            background: white;
            border-radius: 16px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #1a1a1a 0%, #2d2d2d 100%);
            color: white;
            padding: 30px 40px;
            border-bottom: 4px solid #ff6b9d;
        }
        
        .card-number {
            background: #ff6b9d;
            color: white;
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 700;
            display: inline-block;
            margin-bottom: 15px;
        }
        
        .card-title {
            font-size: 2.2rem;
            font-weight: 700;
            margin-bottom: 10px;
        }
        
        .card-subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
            font-style: italic;
        }
        
        .content {
            padding: 40px;
        }
        
        .section {
            margin-bottom: 35px;
        }
        
        .section-header {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #e0e0e0;
        }
        
        .section-icon {
            width: 32px;
            height: 32px;
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            margin-right: 12px;
            font-size: 1.2rem;
        }
        
        .section-title {
            font-size: 1.3rem;
            font-weight: 700;
            color: #1a1a1a;
        }
        
        .mandate-box {
            background: linear-gradient(135deg, #fff5f7 0%, #ffe6ed 100%);
            border-left: 5px solid #f5576c;
            padding: 20px;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            color: #1a1a1a;
        }
        
        .control-box {
            background: #f8f0ff;
            border: 2px solid #9c27b0;
            padding: 20px;
            border-radius: 8px;
            font-size: 1.05rem;
            color: #1a1a1a;
        }
        
        .data-matrix {
            margin-top: 20px;
            overflow-x: auto;
        }
        
        .matrix-table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 8px;
            overflow: hidden;
        }
        
        .matrix-table th {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 12px;
            text-align: left;
            font-weight: 700;
        }
        
        .matrix-table td {
            padding: 12px;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .matrix-table tr:hover {
            background: #f8f9fa;
        }
        
        .permission-badge {
            display: inline-block;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 0.85rem;
            font-weight: 600;
        }
        
        .permission-badge.allow {
            background: #d4edda;
            color: #155724;
        }
        
        .permission-badge.deny {
            background: #f8d7da;
            color: #721c24;
        }
        
        .permission-badge.gate {
            background: #fff3cd;
            color: #856404;
        }
        
        .execution-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 15px;
        }
        
        .execution-item {
            background: #f8f9fa;
            border-left: 4px solid #f093fb;
            padding: 15px;
            border-radius: 6px;
        }
        
        .execution-number {
            background: #f093fb;
            color: white;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-size: 0.85rem;
            font-weight: bold;
            margin-right: 8px;
        }
        
        .code-block {
            background: #1a1a1a;
            color: #ff6b9d;
            padding: 20px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            overflow-x: auto;
            margin-top: 15px;
            line-height: 1.8;
        }
        
        .code-comment {
            color: #888;
        }
        
        .test-grid {
            display: grid;
            gap: 15px;
            margin-top: 15px;
        }
        
        .test-item {
            background: white;
            border: 2px solid #e0e0e0;
            padding: 15px;
            border-radius: 8px;
        }
        
        .test-item.pass {
            border-color: #4caf50;
            background: #f1f8f4;
        }
        
        .test-item.fail {
            border-color: #f44336;
            background: #fef1f0;
        }
        
        .test-label {
            font-weight: 700;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
        }
        
        .test-label.pass::before {
            content: '✓';
            color: #4caf50;
            font-size: 1.5rem;
            margin-right: 8px;
        }
        
        .test-label.fail::before {
            content: '✗';
            color: #f44336;
            font-size: 1.5rem;
            margin-right: 8px;
        }
        
        .context-box {
            background: #fff9e6;
            border: 2px solid #ffcc00;
            padding: 20px;
            border-radius: 8px;
            margin-top: 15px;
        }
        
        .context-title {
            font-weight: 700;
            color: #cc9900;
            margin-bottom: 10px;
            font-size: 1.1rem;
        }
        
        .context-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            margin-top: 10px;
        }
        
        .context-item {
            font-size: 0.95rem;
        }
        
        .context-label {
            font-weight: 600;
            color: #1a1a1a;
        }
        
        .footer {
            background: #f8f9fa;
            padding: 25px 40px;
            border-top: 2px solid #e0e0e0;
        }
        
        .ucf-lineage {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }
        
        .lineage-item {
            background: white;
            padding: 15px;
            border-radius: 6px;
            border-left: 4px solid #f093fb;
        }
        
        .lineage-label {
            font-size: 0.8rem;
            color: #666;
            text-transform: uppercase;
            font-weight: 700;
            margin-bottom: 5px;
        }
        
        .lineage-value {
            font-size: 0.95rem;
            color: #1a1a1a;
            font-weight: 600;
        }
        
        .options-list {
            list-style: none;
            padding: 0;
            margin-top: 10px;
        }
        
        .options-list li {
            padding: 8px 0;
            padding-left: 24px;
            position: relative;
        }
        
        .options-list li::before {
            content: '→';
            position: absolute;
            left: 0;
            color: #f093fb;
            font-weight: bold;
        }
        
        @media print {
            body {
                background: white;
                padding: 0;
            }
            
            .card {
                box-shadow: none;
                max-width: 100%;
            }
        }
        
        @media (max-width: 768px) {
            .execution-grid,
            .context-grid {
                grid-template-columns: 1fr;
            }
            
            .content {
                padding: 20px;
            }
            
            .header {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="card">
        <div class="header">
            <div class="card-number">FRONTIER BOUNDARY CARD #2</div>
            <h1 class="card-title">Data Access Control</h1>
            <p class="card-subtitle">Agents access data based on purpose, not blanket permissions</p>
        </div>
        
        <div class="content">
            <!-- Mandate Section -->
            <div class="section">
                <div class="section-header">
                    <div class="section-icon">📋</div>
                    <h2 class="section-title">Mandate (What Must Be True)</h2>
                </div>
                <div class="mandate-box">
                    AI agents must access customer data only for explicitly authorized purposes. Access rights follow purpose limitation principles: support agents read support data, not marketing profiles; analytics agents read aggregates, not individual records.
                </div>
            </div>
            
            <!-- Control Section -->
            <div class="section">
                <div class="section-header">
                    <div class="section-icon">🔒</div>
                    <h2 class="section-title">Control (Governance Layer)</h2>
                </div>
                <div class="control-box">
                    <strong>Rule:</strong> Implement context-aware data access control using purpose classification:<br><br>
                    1. Tag all data with sensitivity level (Public, Internal, Confidential, Restricted)<br>
                    2. Classify agent purpose at runtime (Support, Analytics, Marketing, Finance)<br>
                    3. Enforce access matrix: purpose × data sensitivity = allow/deny/gate<br>
                    4. Log every data access with purpose justification<br>
                    5. Block cross-purpose data access unless human-authorized
                </div>
                
                <div class="data-matrix">
                    <table class="matrix-table">
                        <thead>
                            <tr>
                                <th>Agent Purpose</th>
                                <th>Public Data</th>
                                <th>Internal Data</th>
                                <th>Confidential Data</th>
                                <th>Restricted Data</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><strong>Support Agent</strong></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge gate">HUMAN GATE</span></td>
                                <td><span class="permission-badge deny">DENY</span></td>
                            </tr>
                            <tr>
                                <td><strong>Analytics Agent</strong></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge allow">ALLOW (Aggregate)</span></td>
                                <td><span class="permission-badge deny">DENY</span></td>
                                <td><span class="permission-badge deny">DENY</span></td>
                            </tr>
                            <tr>
                                <td><strong>Marketing Agent</strong></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge gate">HUMAN GATE</span></td>
                                <td><span class="permission-badge deny">DENY</span></td>
                                <td><span class="permission-badge deny">DENY</span></td>
                            </tr>
                            <tr>
                                <td><strong>Finance Agent</strong></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge allow">ALLOW</span></td>
                                <td><span class="permission-badge gate">HUMAN GATE</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            
            <!-- Execution Section -->
            <div class="section">
                <div class="section-header">
                    <div class="section-icon">⚙️</div>
                    <h2 class="section-title">Agentic Execution Layer</h2>
                </div>
                
                <div class="execution-grid">
                    <div class="execution-item">
                        <span class="execution-number">1</span>
                        <strong>Classify Agent Purpose</strong><br>
                        <span style="font-size: 0.9rem;">Extract agent role from context: support ticket, analytics query, marketing campaign</span>
                    </div>
                    
                    <div class="execution-item">
                        <span class="execution-number">2</span>
                        <strong>Identify Data Sensitivity</strong><br>
                        <span style="font-size: 0.9rem;">Check data classification tags before access attempt</span>
                    </div>
                    
                    <div class="execution-item">
                        <span class="execution-number">3</span>
                        <strong>Matrix Lookup</strong><br>
                        <span style="font-size: 0.9rem;">Query access control matrix: purpose × sensitivity = permission level</span>
                    </div>
                    
                    <div class="execution-item">
                        <span class="execution-number">4</span>
                        <strong>Enforce Decision</strong><br>
                        <span style="font-size: 0.9rem;">ALLOW: grant access. DENY: block with error. GATE: route to human approver</span>
                    </div>
                    
                    <div class="execution-item">
                        <span class="execution-number">5</span>
                        <strong>Log Access Event</strong><br>
                        <span style="font-size: 0.9rem;">Record: timestamp, agent ID, data accessed, purpose, permission granted</span>
                    </div>
                    
                    <div class="execution-item">
                        <span class="execution-number">6</span>
                        <strong>Audit Trail</strong><br>
                        <span style="font-size: 0.9rem;">Store in immutable log for compliance review and anomaly detection</span>
                    </div>
                </div>
                
                <div class="code-block">
<span class="code-comment"># Python Implementation Pattern</span>
<strong>class</strong> DataAccessBoundary:
    <strong>def __init__</strong>(self, access_matrix, audit_log):
        self.matrix = access_matrix
        self.audit = audit_log
    
    <strong>def</strong> check_access(self, agent_id, data_resource, context):
        <span class="code-comment"># Step 1: Classify agent purpose from context</span>
        agent_purpose = self.classify_purpose(agent_id, context)
        <span class="code-comment"># e.g., "support", "analytics", "marketing", "finance"</span>
        
        <span class="code-comment"># Step 2: Get data sensitivity level</span>
        data_sensitivity = self.get_sensitivity(data_resource)
        <span class="code-comment"># e.g., "public", "internal", "confidential", "restricted"</span>
        
        <span class="code-comment"># Step 3: Look up permission in matrix</span>
        permission = self.matrix.get(agent_purpose, data_sensitivity)
        <span class="code-comment"># Returns: "allow", "deny", or "human_gate"</span>
        
        <span class="code-comment"># Step 4: Enforce decision</span>
        <strong>if</strong> permission == "allow":
            self.audit.log({
                "timestamp": datetime.now(),
                "agent_id": agent_id,
                "purpose": agent_purpose,
                "data": data_resource,
                "sensitivity": data_sensitivity,
                "decision": "granted"
            })
            <strong>return</strong> {"access": True, "data": self.fetch_data(data_resource)}
        
        <strong>elif</strong> permission == "deny":
            self.audit.log({
                "timestamp": datetime.now(),
                "agent_id": agent_id,
                "purpose": agent_purpose,
                "data": data_resource,
                "sensitivity": data_sensitivity,
                "decision": "denied"
            })
            <strong>raise</strong> PermissionError(
                f"Agent {agent_id} denied access to {data_sensitivity} data "
                f"for {agent_purpose} purpose"
            )
        
        <strong>elif</strong> permission == "human_gate":
            <span class="code-comment"># Request human approval</span>
            approval = self.request_approval(
                agent_id, 
                agent_purpose, 
                data_resource, 
                data_sensitivity,
                reason=context.get("justification")
            )
            
            <strong>if</strong> approval.granted:
                self.audit.log({
                    "timestamp": datetime.now(),
                    "agent_id": agent_id,
                    "purpose": agent_purpose,
                    "data": data_resource,
                    "decision": "human_approved",
                    "approver_id": approval.approver_id
                })
                <strong>return</strong> {"access": True, "data": self.fetch_data(data_resource)}
            <strong>else</strong>:
                self.audit.log({
                    "timestamp": datetime.now(),
                    "decision": "human_denied",
                    "reason": approval.denial_reason
                })
                <strong>raise</strong> PermissionError(f"Access denied by {approval.approver_id}")
    
    <strong>def</strong> classify_purpose(self, agent_id, context):
        <span class="code-comment"># Implementation: analyze context to determine agent purpose</span>
        <strong>if</strong> "ticket_id" <strong>in</strong> context:
            <strong>return</strong> "support"
        <strong>elif</strong> "report_id" <strong>in</strong> context:
            <strong>return</strong> "analytics"
        <strong>elif</strong> "campaign_id" <strong>in</strong> context:
            <strong>return</strong> "marketing"
        <strong>elif</strong> "transaction_id" <strong>in</strong> context:
            <strong>return</strong> "finance"
        <strong>else</strong>:
            <strong>raise</strong> ValueError("Cannot classify agent purpose from context")
                </div>
            </div>
            
            <!-- Test Section -->
            <div class="section">
                <div class="section-header">
                    <div class="section-icon">✓</div>
                    <h2 class="section-title">Test Framework (Runtime Validation)</h2>
                </div>
                
                <div class="test-grid">
                    <div class="test-item pass">
                        <div class="test-label pass">PASS: Purpose-Based Access</div>
                        <div>Support agent requests customer contact info (Internal data) while resolving ticket. System classifies purpose as "support", checks matrix (Support × Internal = ALLOW), grants access, logs event with ticket ID as justification.</div>
                    </div>
                    
                    <div class="test-item fail">
                        <div class="test-label fail">FAIL: Cross-Purpose Data Leak</div>
                        <div>Marketing agent attempts to access customer support ticket history (Confidential data) without human approval. System must block access (Marketing × Confidential = DENY) and log security violation.</div>
                    </div>
                    
                    <div class="test-item pass">
                        <div class="test-label pass">PASS: Human Gate for Sensitive Access</div>
                        <div>Support agent needs customer financial data (Confidential). System triggers human gate (Support × Confidential = GATE), notifies supervisor, waits for approval with 3-minute timeout, grants access only with authorization.</div>
                    </div>
                    
                    <div class="test-item fail">
                        <div class="test-label fail">FAIL: Missing Purpose Classification</div>
                        <div>Agent makes data request without clear context (no ticket_id, campaign_id, etc.). System must deny access by default and require explicit purpose declaration.</div>
                    </div>
                    
                    <div class="test-item pass">
                        <div class="test-label pass">PASS: Aggregate-Only Analytics</div>
                        <div>Analytics agent requests Internal data. System grants access but automatically filters to aggregate/anonymized view (Analytics × Internal = ALLOW Aggregate). Individual records remain inaccessible.</div>
                    </div>
                    
                    <div class="test-item fail">
                        <div class="test-label fail">FAIL: Incomplete Audit Trail</div>
                        <div>Access granted but audit log missing purpose justification or sensitivity level. System must enforce complete logging for all access events.</div>
                    </div>
                </div>
                
                <div class="context-box" style="margin-top: 20px;">
                    <div class="context-title">⚡ Performance & Scale Requirements</div>
                    <div class="context-grid">
                        <div class="context-item">
                            <span class="context-label">Matrix Lookup:</span> < 10ms per access check
                        </div>
                        <div class="context-item">
                            <span class="context-label">Audit Log Write:</span> Asynchronous, < 100ms
                        </div>
                        <div class="context-item">
                            <span class="context-label">Human Gate Timeout:</span> 3 minutes → auto-deny
                        </div>
                        <div class="context-item">
                            <span class="context-label">Purpose Classification:</span> < 50ms per request
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Business Context -->
            <div class="section">
                <div class="section-header">
                    <div class="section-icon">💼</div>
                    <h2 class="section-title">Business Context & ROI</h2>
                </div>
                
                <div class="context-box">
                    <div class="context-title">When You Need This Boundary</div>
                    <ul class="options-list">
                        <li><strong>Multi-purpose AI systems:</strong> Different agents serving support, analytics, marketing with shared data access</li>
                        <li><strong>Regulated data environments:</strong> GDPR, HIPAA, CCPA requiring purpose limitation and access controls</li>
                        <li><strong>Customer trust scenarios:</strong> Users expect support agents can't access their purchase history for marketing</li>
                        <li><strong>Internal compliance:</strong> SOC 2, ISO 27001 audits requiring documented access controls</li>
                    </ul>
                </div>
                
                <div class="context-box" style="margin-top: 15px;">
                    <div class="context-title">Implementation Effort & ROI</div>
                    <div class="context-grid">
                        <div class="context-item">
                            <span class="context-label">Development Time:</span> 3-5 days (including data classification)
                        </div>
                        <div class="context-item">
                            <span class="context-label">Ongoing Maintenance:</span> 2-4 hours/month (matrix updates)
                        </div>
                        <div class="context-item">
                            <span class="context-label">Risk Without It:</span> GDPR fines (€20M or 4% revenue), data breach lawsuits
                        </div>
                        <div class="context-item">
                            <span class="context-label">Typical ROI:</span> Prevents 1 compliance violation = 100-1000x implementation cost
                        </div>
                    </div>
                </div>
                
                <div class="context-box" style="margin-top: 15px;">
                    <div class="context-title">🚨 Real-World Disaster Prevention</div>
                    <p style="margin-top: 10px; font-size: 0.95rem;"><strong>Case:</strong> A B2B SaaS company's "analytics agent" accessed individual customer contracts (Confidential) to generate usage reports. Sales team inadvertently saw competitor pricing strategies. Result: $2.3M lawsuit, 3 lost enterprise contracts, 18 months rebuilding trust.</p>
                    <p style="margin-top: 10px; font-size: 0.95rem; color: #4caf50;"><strong>Prevention:</strong> Data Access Boundary would have blocked analytics agent from accessing contract-level data (Analytics × Confidential = DENY), limiting to aggregate metrics only.</p>
                </div>
            </div>
        </div>
        
        <!-- Footer -->
        <div class="footer">
            <div class="ucf-lineage">
                <div class="lineage-item">
                    <div class="lineage-label">UCF Lineage</div>
                    <div class="lineage-value">Common Control: AC-03 (Access Enforcement)</div>
                </div>
                
                <div class="lineage-item">
                    <div class="lineage-label">Compliance Mapping</div>
                    <div class="lineage-value">GDPR Art. 5(1)(b), SOC 2 CC6.1, HIPAA §164.308</div>
                </div>
                
                <div class="lineage-item">
                    <div class="lineage-label">Patent Foundation</div>
                    <div class="lineage-value">US9009197B2 - Context-Aware Access Control</div>
                </div>
                
                <div class="lineage-item">
                    <div class="lineage-label">Schema Integration</div>
                    <div class="lineage-value">UCF Purpose Limitation Schema v3.8</div>
                </div>
            </div>
            
            <div style="margin-top: 20px; padding-top: 20px; border-top: 1px solid #ddd; text-align: center; color: #666; font-size: 0.9rem;">
                <strong>Frontier Founder OS: The Governed Agent</strong> • Co-authored by Dorian Cougias & George Martins • © 2025
            </div>
        </div>
    </div>
</body>
</html>
