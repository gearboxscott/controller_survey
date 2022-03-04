controller_surveys Project
=========

Demostrate how to use controller job template surveys

Requirements
------------

none

controller_surveys Variables
--------------

* `survey_name: ''`
* `survey_password: ''`
* `survey_choices: ''`
```
dog
cat
fish
bird
```
* `survey_multiple_choices: ''`
```
formula 1
nascar
indy car
cart
```
* `survey_choice_indexed: ''`
```
VLAN1: 10.10.2.0/24
VLAN2: 10.10.3.0/23
VLAN3: 10.10.10.0/24
VLAN4: 10.10.11.0/24
```

controller_surveys Survey Questions
--------------

```yaml
    survey_spec:
      description: ''
      name: ''
      spec:
      - choices: ''
        default: Tiger Woods
        formattedChoices:
        - choice: ''
          id: 0
          isDefault: false
        max: 1024
        min: 0
        new_question: false
        question_description: ''
        question_name: Enter Name
        required: true
        type: text
        variable: survey_name
      - choices: ''
        default: ''
        max: 1024
        min: 0
        new_question: true
        question_description: ''
        question_name: Enter Password
        required: true
        type: password
        variable: survey_password
      - choices: 'dog

          cat

          fish

          bird'
        default: cat
        formattedChoices:
        - choice: dog
          id: 0
          isDefault: false
        - choice: cat
          id: 1
          isDefault: true
        - choice: fish
          id: 2
          isDefault: false
        - choice: bird
          id: 3
          isDefault: false
        max: 1024
        min: 0
        new_question: false
        question_description: ''
        question_name: Pick One
        required: true
        type: multiplechoice
        variable: survey_choices
      - choices: 'Formula 1

          NASCAR

          Indy Car

          CART'
        default: 'Formula 1

          Indy Car'
        max: 1024
        min: 0
        new_question: true
        question_description: ''
        question_name: Pick Car Racing Series
        required: true
        type: multiselect
        variable: survey_multiple_choices
      - choices: 'VLAN1: 10.10.2.0/24

          VLAN2: 10.10.3.0/24

          VLAN3: 10.10.10.0/24

          VLAN4: 10.10.11:0/24'
        default: 'VLAN3: 10.10.10.0/24'
        max: 1024
        min: 0
        new_question: true
        question_description: ''
        question_name: Pick a VLAN
        required: true
        type: multiselect
        variable: survey_choice_indexed
```

Job Output
------------

```java
Identity added: /runner/artifacts/212/ssh_key_data (/runner/artifacts/212/ssh_key_data)
SSH password: 

PLAY [Project controller_surveys] **********************************************

TASK [print survey_name] *******************************************************
ok: [rhel7test.digitalanvil.local] => {
    "msg": "name: Tiger Woods"
}

TASK [print survey_password] ***************************************************
ok: [rhel7test.digitalanvil.local] => {
    "msg": "password: redhat123"
}

TASK [print choices - single select] *******************************************
ok: [rhel7test.digitalanvil.local] => {
    "msg": "single select: cat"
}

TASK [print choices - multiple select] *****************************************
ok: [rhel7test.digitalanvil.local] => {
    "msg": "multiple select: ['Formula 1', 'Indy Car']"
}

TASK [print choices - how to use description with value to split out to use value] ***
ok: [rhel7test.digitalanvil.local] => {
    "msg": [
        "VLAN: VLAN3",
        "NETWORK:  10.10.10.0/24"
    ]
}

PLAY RECAP *********************************************************************
localhost : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

Dependencies
------------

None.

controller_surveys Project Playbook
----------------

Including an example of how to use your project (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
  - name: print survey_name
    debug:
      msg: 'name: {{ survey_name }}'

  - name: print survey_password
    debug: 
      msg: 'password: {{ survey_password }}'

  - name: print choices - single select
    debug:
      msg: 'single select: {{ survey_choices }}'

  - name: print choices - multiple select
    debug:
      msg: 'multiple select: {{ survey_multiple_choices }}'

  - name: print choices - multiple select
    debug:
      msg: |
        - "vlan: {{ survey_choice_indexed.split(':')[0] }}"
        - "network: {{ survey_choice_indexed.split(':')[1] }}"
```

License
-------

GPL

Author Information
------------------

Scott Parker (sparker@redhat.com)
