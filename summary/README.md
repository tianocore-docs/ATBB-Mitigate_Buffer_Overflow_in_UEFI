# _Summary_ {#summary}

Below table list a set of core security related feature and their compatibility.

NOTE:

*   BLUE means a production feature which might be enabled in the final production.

*   YELLOW means a debug feature which need be disabled in the final production.

*   “V” means 2 features can be enabled together.

*   “N” means 2 feature must not be enabled together.

*   (*) means this feature is for SMM only.

*   No (*) means this feature can be enabled for DXE or SMM.

![](Mydir/media/image28.png)

SMM static paging feature is the only one what cannot be enabled with other features if the other features need modify the page table.