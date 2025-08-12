# 🌱 Note: Popup to support column adds, reordering, and save view 
##  ⌚️ Date: Aug 4, 2023
##  🎫 Story Ticket: AI-4404

> [!info] Goals:
> > 
> > - [ ] figure out how column order is working
> > - [ ] figure out what component it is in
> > - [ ] understand inputs and outputs and how its talking to the container
> > - [ ] simple
> > 
> >
> > 


# To-do list 📝
---

- [ ] Wake up

- [ ] Eat breakfast

- [x] Brush teeth


# Jot down 📝 
---
_Link:_https://manhattanassociates.atlassian.net/browse/AI-4404

- column view, gear icon, and save view
#### Column View:
Following was found in Allocation :
```html
 <div class="dm-flex-col-layout dm-fill-space center-panel">
        <ion-content class="scroll-panel" name="screen-panel">
          <ng-container *ngIf="isLoading"> </ng-container>
          <card-panel
            [resultList]="searchResults"
            [levelDisplayText]="levelDisplay"
            [search]="search"
            *ngIf="!isLoading"
            [hiddenFilter]="hiddenFilters"
            [navFilters]="navRouteFilters"
          ></card-panel>
        </ion-content>
```
##### card-panel
suggested-allocation/ components/card-panel/card-panel.component.ts
```typeScript
@Component({
  selector: 'card-panel',
  templateUrl: './card-panel.component.html',
  styleUrls: ['./card-panel.component.scss']
})
export class CardPanelComponent extends BaseListPage
  implements OnInit, OnChanges {
  @Input() resultList: SearchResults;
  @Input() search: Search;
  @Input() levelDisplayText: string;
  @Input() hiddenFilter: any;
  @Input() navFilters: any;

```

##### card-view
suggested-allocation/ components/card-view/card-view.component.ts
```typeScript
@Component({
  selector: 'card-view',
  templateUrl: './card-view.component.html',
  styleUrls: ['./card-view.component.scss']
})
export class CardViewComponent extends SizeDetails implements OnInit, OnDestroy {
  @ViewChild('outlet', { read: ViewContainerRef }) outletRef: ViewContainerRef;
  @ViewChild('content', { read: TemplateRef, static: true }) contentRef: TemplateRef<any>;
  @Input() cardDetails: Result;
  @Input() search: Search;
  @Input() levelDisplayText: string;
  @Input() hiddenFilter: any;  
  @Input() navFilters: any;  
```
#### Save View:
ui-sc-common
```typeScript
@Component({
  selector: 'saved-views-modal',
  templateUrl: './saved-views.modal.html',
  styleUrls: ['./saved-views.modal.scss']
})
export class SavedViewsModal extends Overlay implements OnInit {
  @Input() public componentName: string;
  @Input() public viewName: string;
  @Input() public viewType: string;

  @Input() public search: Search;
  @Input() public metaConfig: MetaConfig;
  @Input() public selectedFilter: UserSearch;
  @Input() public componentRef: ComponentRef<SavedViewsModal>;

  @Output() viewChangeEvent: EventEmitter<SavedView> = new EventEmitter();

  @ViewChild('saveView') saveViewBtn;
  @ViewChild('container') container: ElementRef;

```

#### Gear Icon(Metadata Adjustments)
ui/metadata-editor/metadata-editor.component.ts
```typeScript
@Component({
  selector: 'metadata-editor',
  templateUrl: './metadata-editor.component.html',
  styleUrls: ['./metadata-editor.component.scss']
})
export class MetadataEditorComponent implements OnInit, AfterViewInit {

@Input() pageName = '';

title: string;

  

@Input()

componentName = '';

  

@Input()

viewName = '';

  

@Input()

entityName: string;
```
# Sub-pages 📑

---
- [[Sub Page]]
- [[Sub Page]]
- [[Sub Page]]
- [[Sub Page]]

# Reference links 🔗
---

[Beyond Frank Lloyd Wright: A Broader View of Art in Chicago](https://www.nytimes.com/2018/03/08/arts/chicago-museums-art.html?rref=collection%2Fsectioncollection%2Ftravel)

  
[Havana's Symphony of Sound](https://www.nytimes.com/2018/03/12/travel/havana-cuba.html?rref=collection%2Fsectioncollection%2Ftravel)