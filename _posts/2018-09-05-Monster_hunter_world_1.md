---
title: 개인 프로젝트 - Monster hunter world project
description: <center>1. 무기 데이터 입력</center>
categories:
 - Project
tags:
---

개인 프로젝트로 게임 Monster hunter world의 아이템 시뮬레이터를 만들어 보기로 하였다.
전체적인 디렉토리의 트리이다.

<img src="{{ site.url }}/assets/images/project_dir.png" alt="dir_tree" width="30%">

무기에 대한 정보는 이미 엑셀로 정리하여 올려놓은 유저가 있었기에 그 데이터를 참고하여 정리 한 후 사용하였다.
엑셀에서의 데이터를 읽기 위해서는 `openpyxl`이라는 `python package`를 이용하였다.

기본적으로 엑셀을 읽기 위해서
```python
wb = openpyxl.load_workbook(<엑셀파일 이름>)
ws = WB[<sheet 이름>]
for row in range(<row의 길이>):
  for column in range(<column의 길이>):
    ws.cell(row=row, column=column).value
```
위와 같은 코드를 사용하여 cell을 읽어오도록 하였다.

실제로 사용한 코드를 가져온다면

```python
WB = openpyxl.load_workbook('weapon_data.xlsx')


def great_sword():

    ws = WB['Great_Sword']

    for row in range(2, 92):
            name = ws.cell(row=row, column=1).value
            rare = ws.cell(row=row, column=2).value
            produce = ws.cell(row=row, column=3).value
            attack = ws.cell(row=row, column=4).value
            defense = ws.cell(row=row, column=5).value
            if ws.cell(row=row, column=6).value is None:
                weapon_property = '없음'
                weapon_property_fiqure = '없음'
            else:
                weapon_property = ws.cell(row=row, column=6).value
                weapon_property_fiqure = ws.cell(row=row, column=7).value

            if ws.cell(row=row, column=8).value is None:
                abnormal_condition = '없음'
                abnormal_condition_figure = '없음'
            else:
                abnormal_condition = ws.cell(row=row, column=8).value
                abnormal_condition_figure = ws.cell(row=row, column=9).value

            fatal_blow = ws.cell(row=row, column=10).value
            if ws.cell(row=row, column=11).value is None:
                slot = '없음'
            else:
                slot = ws.cell(row=row, column=11).value

            GreatSword.objects.create(
                name=name,
                rare=rare,
                produce=produce,
                attack=attack,
                defense=defense,
                weapon_property=weapon_property,
                weapon_property_fiqure=weapon_property_fiqure,
                abnormal_condition=abnormal_condition,
                abnormal_condition_figure=abnormal_condition_figure,
                fatal_blow=fatal_blow,
                slot=slot,
            )
    print('Great Sword Done')
```

위의 코드와 같이 작성하였지만 cell의 범위를 수동으로 작성해주어야 한다는 점과 sheet의 이름 또한
작성해주어야 한다는 점이 마음에 들지 않아 수정을 할 예정이다.

그리고 또한 수렵피리의 경우 음색에 대한것을 크롤링을 통해 이미지를 가져와서 데이터를 저장해야 할지 아니면
데이터를 간단하게 만들어 저장할지 고민하고 있으며 조충곤의 경우 벌레의 강화를 어떤식으로 정리해야 할지
아직 고민중이다. 또한 궁의 경우 지원하는 병을 어떻게 정리를 하여야 할지에 대해 고민중이며 빠른 시일 내에
해결 할 예정이다.

---
--추가내용<br>
`wb.get_sheet_names()`를 하게되면 모든 sheet를 `list`형식으로 반환한다고 한다. <br>
그렇다면 위의 메서드를 이용하여 전체의 sheet를 순환할 수 있다는 것이다. 하지만 글을 가지고 있는
`row`와 `column`을 알 수 있는 방법을 아직 못 찾았기에 찾기 전까지 보류하려고 한다.
