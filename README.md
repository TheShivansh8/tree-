# tree-
nodes:

  - id: START
    type: start
    text: "Good evening. Let's review your day."

  # ---------------- AXIS 1: LOCUS ----------------

  - id: A1_OPEN
    parentId: START
    type: question
    text: "How would you describe your day overall?"
    options:
      - "Productive"
      - "Mixed"
      - "Frustrating"
      - "Draining"

  - id: A1_DECIDE
    parentId: A1_OPEN
    type: decision
    rules:
      - condition: "answer in ['Productive','Mixed']"
        target: A1_Q1_HIGH
      - condition: "answer in ['Frustrating','Draining']"
        target: A1_Q1_LOW

  - id: A1_Q1_HIGH
    parentId: A1_DECIDE
    type: question
    text: "What contributed most to things going well?"
    options:
      - "I prepared and planned ahead"
      - "The team supported me"
      - "Things just worked out"
      - "I adapted quickly"
    signal:
      - "axis1:internal"
      - "axis1:external"
      - "axis1:external"
      - "axis1:internal"

  - id: A1_Q1_LOW
    parentId: A1_DECIDE
    type: question
    text: "When things went wrong, what was your first reaction?"
    options:
      - "Look for what I could control"
      - "Wait for help"
      - "Blame external factors"
      - "Push through without clarity"
    signal:
      - "axis1:internal"
      - "axis1:external"
      - "axis1:external"
      - "axis1:internal"

  - id: A1_Q2
    parentId: A1_Q1_HIGH
    type: question
    text: "When facing difficulty, what did you do?"
    options:
      - "Adjusted my approach"
      - "Stayed stuck"
      - "Relied on others"
      - "Tried something new"
    signal:
      - "axis1:internal"
      - "axis1:external"
      - "axis1:external"
      - "axis1:internal"

  - id: A1_Q2B
    parentId: A1_Q1_LOW
    type: question
    text: "What best describes your response to challenges?"
    options:
      - "Took ownership"
      - "Felt helpless"
      - "Waited for direction"
      - "Experimented with solutions"
    signal:
      - "axis1:internal"
      - "axis1:external"
      - "axis1:external"
      - "axis1:internal"

  - id: A1_REF_INT
    parentId: A1_Q2
    type: reflection
    text: "You demonstrated agency today. You didn't wait — you acted."
    signal: "axis1:internal"

  - id: A1_REF_EXT
    parentId: A1_Q2B
    type: reflection
    text: "You leaned on external factors today. The question is — where did you still have a choice?"
    signal: "axis1:external"

  - id: BRIDGE_1_2
    parentId: A1_REF_INT
    type: bridge
    text: "Now shift focus — from control to contribution."
    target: A2_OPEN

  - id: BRIDGE_1_2B
    parentId: A1_REF_EXT
    type: bridge
    text: "Now shift focus — from control to contribution."
    target: A2_OPEN

  # ---------------- AXIS 2: CONTRIBUTION ----------------

  - id: A2_OPEN
    type: question
    text: "Think about your interactions today. What stands out?"
    options:
      - "I helped someone"
      - "I did my tasks"
      - "I felt overlooked"
      - "I expected more support"

  - id: A2_Q1
    parentId: A2_OPEN
    type: question
    text: "Which statement best reflects your mindset?"
    options:
      - "I contributed beyond my role"
      - "I did what was required"
      - "I deserved more recognition"
      - "Others should have done more"
    signal:
      - "axis2:contribution"
      - "axis2:neutral"
      - "axis2:entitlement"
      - "axis2:entitlement"

  - id: A2_Q2
    parentId: A2_Q1
    type: question
    text: "How did you respond to others’ needs?"
    options:
      - "Proactively helped"
      - "Helped when asked"
      - "Ignored"
      - "Felt burdened"
    signal:
      - "axis2:contribution"
      - "axis2:neutral"
      - "axis2:entitlement"
      - "axis2:entitlement"

  - id: A2_REF_CONTRIB
    parentId: A2_Q2
    type: reflection
    text: "You showed contribution today. You added value beyond obligation."
    signal: "axis2:contribution"

  - id: A2_REF_ENTITLE
    parentId: A2_Q2
    type: reflection
    text: "There was expectation today. The shift is simple — focus on what you give."
    signal: "axis2:entitlement"

  - id: BRIDGE_2_3
    parentId: A2_REF_CONTRIB
    type: bridge
    text: "Now expand your perspective."
    target: A3_OPEN

  - id: BRIDGE_2_3B
    parentId: A2_REF_ENTITLE
    type: bridge
    text: "Now expand your perspective."
    target: A3_OPEN

  # ---------------- AXIS 3: RADIUS ----------------

  - id: A3_OPEN
    type: question
    text: "When reflecting on today, who do you think about most?"
    options:
      - "Myself"
      - "My team"
      - "A colleague"
      - "The customer"

  - id: A3_Q1
    parentId: A3_OPEN
    type: question
    text: "What mattered most in your decisions today?"
    options:
      - "My workload"
      - "Team success"
      - "Helping someone"
      - "Impact on users"
    signal:
      - "axis3:self"
      - "axis3:team"
      - "axis3:others"
      - "axis3:others"

  - id: A3_Q2
    parentId: A3_Q1
    type: question
    text: "How did you handle challenges?"
    options:
      - "Focused on my stress"
      - "Considered team impact"
      - "Helped others despite pressure"
      - "Balanced all perspectives"
    signal:
      - "axis3:self"
      - "axis3:team"
      - "axis3:others"
      - "axis3:others"

  - id: A3_REF_SELF
    parentId: A3_Q2
    type: reflection
    text: "Your focus stayed narrow today. Expanding perspective reduces pressure."
    signal: "axis3:self"

  - id: A3_REF_OTHER
    parentId: A3_Q2
    type: reflection
    text: "You looked beyond yourself. That’s where meaning compounds."
    signal: "axis3:others"

  # ---------------- SUMMARY ----------------

  - id: SUMMARY
    parentId: A3_REF_OTHER
    type: summary
    text: "Today you showed {axis1.dominant} control, {axis2.dominant} contribution, and {axis3.dominant} perspective."

  - id: END
    parentId: SUMMARY
    type: end
    text: "Session complete. See you tomorrow."
