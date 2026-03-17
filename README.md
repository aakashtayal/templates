# templates
It contains templates for automation

![privatelink_architecture_diagram](https://github.com/user-attachments/assets/d9651434-8027-4164-8d3a-33a62442efc1)
<svg width="100%" viewBox="0 0 680 720" xmlns="http://www.w3.org/2000/svg" style="font-family: sans-serif; background: #ffffff;">
<defs>
  <marker id="arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
    <path d="M2 1L8 5L2 9" fill="none" stroke="context-stroke" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
  <style>
    text { font-family: sans-serif; fill: #2C2C2A; }
    .th { font-size: 14px; font-weight: 500; fill: #0C447C; }
    .ts { font-size: 12px; font-weight: 400; fill: #185FA5; }
    .label { font-size: 12px; font-weight: 400; fill: #444441; }

    .src-outer { fill: #E6F1FB; stroke: #185FA5; }
    .src-inner { fill: #B5D4F4; stroke: #185FA5; }
    .src-th { fill: #0C447C; }
    .src-ts { fill: #185FA5; }

    .dst-outer { fill: #E1F5EE; stroke: #0F6E56; }
    .dst-inner { fill: #9FE1CB; stroke: #0F6E56; }
    .dst-th { fill: #085041; }
    .dst-ts { fill: #0F6E56; }

    .auto-outer { fill: #FAEEDA; stroke: #854F0B; }
    .auto-inner { fill: #FAC775; stroke: #854F0B; }
    .auto-th { fill: #633806; }
    .auto-ts { fill: #854F0B; }

    .gray-inner { fill: #D3D1C7; stroke: #5F5E5A; }
    .gray-th { fill: #444441; }
    .gray-ts { fill: #5F5E5A; }

    .arr { stroke: #5F5E5A; stroke-width: 1.5; fill: none; }
    .dashed { stroke: #BA7517; stroke-width: 1; fill: none; stroke-dasharray: 5 3; }
    .pl-link { stroke: #1D9E75; stroke-width: 1.5; fill: none; }
  </style>
</defs>

<!-- Account labels -->
<text class="label" x="168" y="22" text-anchor="middle">Source account</text>
<text class="label" x="510" y="22" text-anchor="middle">Destination account</text>

<!-- Source VPC outer -->
<rect class="src-outer" x="20" y="30" width="296" height="310" rx="16" stroke-width="0.5"/>
<text class="th src-th" x="36" y="54">Source VPC</text>
<text class="ts src-ts" x="36" y="70">Overlapping CIDR OK</text>

<!-- EC2 instances -->
<rect class="src-inner" x="38" y="82" width="124" height="56" rx="8" stroke-width="0.5"/>
<text class="th src-th" x="100" y="108" text-anchor="middle">EC2 instances</text>
<text class="ts src-ts" x="100" y="126" text-anchor="middle">App connects on :3306</text>

<!-- Arrow EC2 → Interface Endpoint -->
<line class="arr" x1="162" y1="110" x2="186" y2="110" marker-end="url(#arrow)"/>

<!-- Interface Endpoint -->
<rect class="src-inner" x="188" y="82" width="116" height="56" rx="8" stroke-width="0.5"/>
<text class="th src-th" x="246" y="106" text-anchor="middle">Interface</text>
<text class="th src-th" x="246" y="120" text-anchor="middle">Endpoint</text>
<text class="ts src-ts" x="246" y="134" text-anchor="middle">vpce DNS name</text>

<!-- Private subnets -->
<rect class="gray-inner" x="38" y="158" width="266" height="44" rx="8" stroke-width="0.5"/>
<text class="th gray-th" x="171" y="178" text-anchor="middle">Private subnets (min. 2 AZs)</text>
<text class="ts gray-ts" x="171" y="194" text-anchor="middle">No route table changes needed</text>

<!-- Key benefits box -->
<rect class="gray-inner" x="38" y="216" width="266" height="110" rx="8" stroke-width="0.5"/>
<text class="th gray-th" x="171" y="238" text-anchor="middle">Cross-account + cross-region</text>
<text class="ts gray-ts" x="171" y="258" text-anchor="middle">Overlapping CIDR supported</text>
<text class="ts gray-ts" x="171" y="276" text-anchor="middle">No VPC peering required</text>
<text class="ts gray-ts" x="171" y="294" text-anchor="middle">No route table dependencies</text>
<text class="ts gray-ts" x="171" y="312" text-anchor="middle">Multiple EC2 clients supported</text>

<!-- Destination VPC outer -->
<rect class="dst-outer" x="364" y="30" width="296" height="310" rx="16" stroke-width="0.5"/>
<text class="th dst-th" x="380" y="54">Destination VPC</text>
<text class="ts dst-ts" x="380" y="70">Separate AWS account</text>

<!-- Endpoint Service -->
<rect class="dst-inner" x="378" y="82" width="130" height="56" rx="8" stroke-width="0.5"/>
<text class="th dst-th" x="443" y="106" text-anchor="middle">Endpoint service</text>
<text class="ts dst-ts" x="443" y="124" text-anchor="middle">PrivateLink (NLB-backed)</text>

<!-- Arrow Endpoint Service → NLB -->
<line class="arr" x1="508" y1="138" x2="508" y2="158" marker-end="url(#arrow)"/>

<!-- NLB -->
<rect class="dst-inner" x="378" y="160" width="130" height="56" rx="8" stroke-width="0.5"/>
<text class="th dst-th" x="443" y="184" text-anchor="middle">Network LB</text>
<text class="ts dst-ts" x="443" y="202" text-anchor="middle">Internal, TCP :3306</text>

<!-- Arrow NLB → RDS -->
<line class="arr" x1="508" y1="216" x2="508" y2="238" marker-end="url(#arrow)"/>

<!-- RDS -->
<rect class="dst-inner" x="378" y="240" width="130" height="56" rx="8" stroke-width="0.5"/>
<text class="th dst-th" x="443" y="264" text-anchor="middle">RDS / Aurora</text>
<text class="ts dst-ts" x="443" y="282" text-anchor="middle">MySQL :3306</text>

<!-- Target group -->
<rect class="gray-inner" x="524" y="160" width="124" height="56" rx="8" stroke-width="0.5"/>
<text class="th gray-th" x="586" y="184" text-anchor="middle">Target group</text>
<text class="ts gray-ts" x="586" y="202" text-anchor="middle">IP type, :3306</text>

<!-- NLB ↔ Target group dashed -->
<line stroke="#5F5E5A" stroke-width="0.5" stroke-dasharray="4 3" x1="508" y1="188" x2="524" y2="188"/>

<!-- PrivateLink tunnel -->
<path class="pl-link" d="M304 110 L364 110" marker-end="url(#arrow)"/>
<rect x="306" y="94" width="52" height="18" rx="4" fill="#E1F5EE" stroke="#0F6E56" stroke-width="0.5"/>
<text style="font-size:11px; font-weight:500; fill:#085041;" x="332" y="107" text-anchor="middle">AWS PrivateLink</text>

<!-- Automation loop outer -->
<rect class="auto-outer" x="20" y="362" width="640" height="180" rx="16" stroke-width="0.5"/>
<text class="th auto-th" x="36" y="386">Dynamic IP management (destination account)</text>
<text class="ts auto-ts" x="36" y="402">Keeps NLB target group in sync when RDS IP changes</text>

<!-- RDS Event Subscription -->
<rect class="auto-inner" x="38" y="412" width="138" height="56" rx="8" stroke-width="0.5"/>
<text class="th auto-th" x="107" y="432" text-anchor="middle">RDS event</text>
<text class="th auto-th" x="107" y="448" text-anchor="middle">subscription</text>
<text class="ts auto-ts" x="107" y="464" text-anchor="middle">failover, maintenance…</text>

<!-- Arrow Event → SNS -->
<line class="arr" x1="176" y1="440" x2="210" y2="440" marker-end="url(#arrow)"/>

<!-- SNS Topic -->
<rect class="auto-inner" x="212" y="412" width="110" height="56" rx="8" stroke-width="0.5"/>
<text class="th auto-th" x="267" y="434" text-anchor="middle">SNS topic</text>
<text class="ts auto-ts" x="267" y="452" text-anchor="middle">Triggers on event</text>

<!-- Arrow SNS → Lambda -->
<line class="arr" x1="322" y1="440" x2="356" y2="440" marker-end="url(#arrow)"/>

<!-- Lambda -->
<rect class="auto-inner" x="358" y="412" width="140" height="56" rx="8" stroke-width="0.5"/>
<text class="th auto-th" x="428" y="430" text-anchor="middle">Lambda function</text>
<text class="ts auto-ts" x="428" y="448" text-anchor="middle">nslookup RDS endpoint</text>
<text class="ts auto-ts" x="428" y="464" text-anchor="middle">→ updates target group IP</text>

<!-- Lambda → Target Group (dashed return) -->
<path class="dashed" d="M498 412 L498 390 L586 390 L586 360" marker-end="url(#arrow)"/>

<!-- RDS fires events (dashed return) -->
<path class="dashed" d="M443 360 L443 390 L107 390 L107 468" marker-end="url(#arrow)"/>

</svg>
