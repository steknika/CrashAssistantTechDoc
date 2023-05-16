# Crash Assistant Technical Documentation

*Created by István Karpács, 2023*

## Table of content

- [Introduction](#introduction)
  
  - [Purpose of the documentation](#purpose-of-the-documentation)

- [Use of the Crash Assistant screens](#use-of-the-crash-assistant-screens)
  
  - [How to reach the Crash Assistant](#how-to-reach-the-crash-assistant)
  
  - [Collect crash info](#collect-crash-info)
  
  - [Who was injured](#who-was-injured)
  
  - [Other drivers info](#other-drivers-info)
  
  - [Your info](#your-info)
  
  - [Crash report](#crash-report)

- [Folder structure](#folder-structure)

- [Entry points](#entry-points)

- [Architecture](#architecture)
  
  - [ViewControllers](#viewcontrollers)
    
    - [CrashAssistantViewController](#crashassistantviewcontroller)
    
    - [CrashAssistantModalViewController](#crashassistantmodalciewcontroller)
    
    - [CrashAssistantInjuryViewController](#crashassistantinjuryviewcontroller)
  
  - [Views](#views)
  
  - [TableViews](#tableviews)
  
  - [ViewModels](#viewmodels)
  
  - [Datas](#datas)
  
  - [Protocols](#protocols)
  
  - [Delegates](#delegates)

## Introduction

The `Crash Assistant` is a software solution that assists users in gathering information about a crash site. By generating a crash report, this tool provides images of the scene that can be used for potential claims or repair estimations. This feature enhances the user's ability to collect data accurately and efficiently, making the process smoother and more convenient.

### Purpose of the documentation

The goal of this documentation is to provide a comprehensive guide for future programmers who will be adding new functionalities to the system. It also serves as a reference for efficiently making changes to specific parts of the code without requiring a deep understanding of every detail. By using this documentation, programmers can save time and effort, and easily maintain and enhance the system.

## Use of the Crash Assistant screens

Maintaining code quality is essential, and one of the ways to achieve it is by understanding how end users will interact with the `Crash Assistant`. To facilitate this understanding, we have created a user guide that presents all the necessary information about how to use the interface and what outcomes are expected. By providing this information, developers can ensure that the system functions properly and efficiently, and end-users can utilize the tool effectively.

### How to reach the Crash Assistant

Accessing the `Crash Assistant` screen can be done through various methods, including:

- `SMS Deeplink` which is sent by the server when a crash event is detected
- `Assistance` feature from the bottom Tab bar
  - Selecting the `Crash Assistant`option
  - Selecting a draft from the `View Crash Reports` option

These options provide users with flexibility in accessing the `Crash Assistant`, and enable them to quickly and conveniently utilize its features.

### Collect Crash Info

The `Crash Assistant` screen, titled as `Collect Crash Info` feature comprises several selectable categories and buttons, including:

- `Who was injured?`: This category screen enables users to identify injured persons by selecting them.

- `Other driver's info`: This category screen allows users to provide information about the opposite driver, as well as the damages sustained by their vehicle during the accident.

- `Collect your info`: This category screen enables users to collect information about their own vehicle damages, as well as the crash scene.

- `Create crash report` button located at the bottom of the screen, which becomes active once at least one piece of information has been provided in the above options. This button is used to generate a crash report.

- `Information` button located on the top right corner of the navigation bar, represented by an `i` character in a circle. This button enables users to revisit the `Emergency Checklist` at any time.

- `Close` button located on the top left corner of the navigation bar, represented by an `X`. This button provides users with options to either `Keep editing`, `Save as draft`, or `Discard` the current crash report in progress.

### Who was injured

This section provides information on how to select the injured party in an accident report.

There are six options available for selection:

- `Myself`
- `My Passenger(s)`
- `Other driver`
- `Other driver passenger(s)`
- `No One`
- `Unsure`

To save the selection, click the "Done" button. If the selection needs to be discarded, click the close button.

### Other drivers info

This screen has multiple section, where you can add images, based on the section title.

- `License / Insurance info`

- `Vehicle's licence plate`

- `Vehicle's damages`

- `Additional note`
  
  To save the images, click the `Done` button. If the selection needs to be discarded, click the close button.

### Your info

This screen has multiple section, where you can add images, based on the section title.

- `Your vehicle's damages`

- `Crash scene photos`

To save the images, click the `Done` button. If the selection needs to be discarded, click the close button.

### Crash report

The `Crash Report` screen has two buttons:

- `View Crash Report`

- `Share Crash Report`

When all the interaction is finished, you can use

## Folder Structure

The `Crash Assistant` can be found under the following folder structure:

```swift
ConsumerCrash-iOS\ViewControllers\CrashAssistantNewFlow
```

Inside this folder, there will be several levels of subfolders and files. This documentation gives small description to the files, so it can be identified by its behaviour and responsibility.

- `.\Base`: This folder contains all of the basic ingredients for the `Crash Assistant`
  
  - `.\BaseInformation`
    
    - `BaseCrashAssistTableView.swift`: this is the basic building block for all the tableView-s in the Crash Assistant
    
    - `CrashAssistModalTableView.swift`: typealias for combining the `BaseCrashAssistTableView` and `CrashAssistModalTableViewProtocol`
    
    - `CrashAssistModalTableViewProtocol.swift`: all of the initializations which is needed to create a `tableView` in this architecture.
    
    - `.\Delegate`
      
      - `BaseCrashAssistTableViewDelegate.swift`: delegate to enable user interaction when needed on a screen.
  
  - `.\Delegate`
    
    - `CrashAssistImagePickerDelegate.swift`: image delegate that is used for adding and manipulating images in the crash assistant
  
  - `.\InfoCells`: these are the cells that is used for the sections. All of the above cells are `CrashAssistantGeneralCell` and the usage and creation of these cell are discussed in the [Views](#views) .
    
    - `CrashAssistImageCell.swift`: that is used for presenting images and using the logic. Using `ImageCollectionStackViewWithTitle`.
    
    - `CrashAssistNoteCell.swift`: for presenting and manipulating a titleLabel using `SimpleTitleView`
    
    - `CrashAssistTextViewCell.swift`: for presenting and manipulating `textView`. Using `BorderedTextView`
    
    - `CrashAssistTitleCell.swift`: presenting the title and a cirlce image, which can be set for a checkmark. `TitleAndDescriptionCheckMarkView`

- `.\GeneralLocalCell`
  
  - `CrashAssistantGeneralCell.swift`
  
  - `.\Protocol`
    
    - `CrashAssistantGeneralCellProtocol.swift`
    
    - `CrashAssistantImageCellProtocol.swift`
    
    - `CrashAssistantTitleCellProtocol.swift`

- `.\Model`
  
  - `.\Action`
    
    - `CrashAssistAction.swift`
    
    - `CrashAssistActionEnum.swift`
  
  - `.\Data`
    
    - `CrashAssistantInjuryData.swift`
    
    - `CrashAssistantOtherDriverData.swift`
    
    - `CrashAssistantReportData.swift`
    
    - `CrashAssistantUserData.swift`
    
    - `CrashAssistCrashIdData.swift`
    
    - `CrashAssistCrashListData.swift`
    
    - `CrashAssistCrashSceneData.swift`
    
    - `CrashAssistDeleteResponseData.swift`
    
    - `CrashAssistFileStorageData.swift`
  
  - `.\SectionCellViewModel`
    
    - `.\SectionType`
      
      - `CrashAssistantSectionType.swift`
    
    - `.\Protocol`
      
      - `CrashAssistantCellViewModelProtocol.swift`
      
      - `CrashAssistantSectionViewModelProtocol.swift`
    
    - `.\Implementation`
      
      - `CrashAssistantCellViewModel.swift`
      
      - `CrashAssistantSectionViewModel.swift`

- `.\ViewModel`
  
  - `CrashAssistCategoryViewModel.swift`
  
  - `.\Protocol`
    
    - `CrashAssistantTableViewModelProtocol.swift`
    
    - `CrashAssistantViewModelProtocol.swift`
    
    - `CrashAssistCategoryViewModelProtocol.swift`
    
    - `UpdateSectionInfoViewModelProtocol`
  
  - `.\ViewModelCreator`
    
    - `CrashAssistantViewModelCreator.swift`

- `.\Views`
  
  - `.\InjuryInformation`
    
    - `.\ViewController`
    
    - `.\ViewModel`
  
  - `.\OtherDriverInformation`
    
    - `.\TableView`
    
    - `.\ViewModel`
  
  - `.\UserInformation`
    
    - `.\TableView`
    
    - `.\ViewModel`

- `.\ViewControllers`
  
  - `.\CrashAssistCategoryTableView`
  
  - `.\CrashReport`
  
  - `.\Delegate`
  
  - `.\PDFViewer`
  
  - `.\PermissionViewController`
  
  - `.\Protocol`

Some of the required `Views` can be found at:

```swift
ConsumerCrash-iOS\ViewControllers\Views\GeneralViews
```

## Entry points

The `Crash Assistant` entry can be find called from two places.

`CrashAssistanceMainMenuViewController.swift`:

```swift
func openCrashAssistantHomeScreen(showCheckList: Bool) {
    let crashAssistantViewController = CrashAssistantViewController(
        viewModel: CrashAssistantViewModelCreator().getViewModel(),
        localDataManager: LocalDataManager(),
        showCheckList: showCheckList)
    let nav = UINavigationController(rootViewController:crashAssistantViewController)
    nav.modalPresentationStyle = .fullScreen
    present(nav, animated: true)
}
```

This function is called when the user accesses the `Crash Assistant` screen from the Assistance menu.

`CrashReportsViewController.swift`

```swift
private func presentCrashAssistant(crashDraftReport: CrashAssistCrashListData) {
    let crashAssistantViewController = CrashAssistantViewController(
        viewModel: CrashAssistantViewModelCreator().getViewModel(),
        localDataManager: LocalDataManager(),
        showCheckList: true,
        draftData: crashDraftReport)
    let nav = UINavigationController(rootViewController: crashAssistantViewController)
    nav.modalPresentationStyle = .fullScreen
    present(nav, animated: true)
}
```

This function is called, when the user want to continue a draft report, from the `View Crash Report` screen.

## Architecture

The architecture of the `Crash Assistant` feature attempts to adhere to multiple design patterns and maintain consistency with the SOLID principles, even though it may not always be sustainable in certain areas.

The initial concept was to utilize object composition to minimize communication problems between elements. This approach helps to eliminate potential retain cycles. However, it also introduces additional complexity, which will be discussed in more detail later in the [Delegates](#delegates) section.

*NOTE: This not a fully **Composition over inheritance** thinking, because inheritence plays a main role in a lot of aspects of this feature. Using **Composition** and **inheritence** together can be really powerful.*

**The basic principle is that every object can communicate directly with its children, but every child needs to use a delegate to communicate with its parent. This is necessary so that low-level components are not dependent on high-level components. Also all the child component should be a protocol if it is maintainable, following the Liskov Substitution Principle.**

*IMPORTANT NOTE: every communication has only one-level forward or backward. There is no multi-level communication in the `Crash Assistant` feature. This allows objects to maintain their responsibilities more easily, and keeps the code cleaner and more bug-free, but also adds to the complexity and creates a lot more extra files in the process. However, it is crucial to maintain this type of communication in the future to prevent unwanted bugs and behaviors.*

The `viewModel` is a crucial component in the `Crash Assistant` architecture. It acts as a bridge between the view and the model, and holds all the necessary data and logic required to render a particular view. The `viewModel` can offer two main functionalities:

- **Holding information of the views and structures**: The `viewModel` can hold information about the views that will be displayed, such as the text to be displayed, the layout of the views, and the types of controls to be used. It can also hold information about the structure of the views, such as how the views are nested and how they interact with each other.

- **Updating data and creating specific data based on the information one possesses**: The `viewModel` can update data based on user inputs or other events. It can also create specific data based on the information it possesses. For example, the `viewModel` can create the `crashReportData` that is required for completing a crash report.

Overall, the `viewModel` plays a crucial role in separating the view from the model, and in keeping the code clean and modular. In the next section, we will discuss the `viewModel` in more details.

### ViewControllers

Inside the `Crash Assistant` folder, there are several files and folders, but for the purpose of this section, we will focus on the five ViewControllers that exist within the `CrashAssistantNewFlow` folder:

- `CrashAssistantViewController`
- `CrashAssistantModalViewController`
- `CrashAssistantInjuryViewController`
- `PDFViewer`
- `CameraPermissionViewController`

*NOTE: there is one additional viewController, the `CrashAssistantChecklistViewController`, which is not presented in this list. This is because it is not in the hierarchy of the `CrashAssistantNewFlow` folder structure. However, it should be moved later on to this folder from `~\CrashAssistance\CheckList\CrashAssistantChecklistViewController.swift`.*

In this section, we will only focus on the first three viewControllers presented in the list. We will discuss their responsibilities, functionalities, and behaviors.

### CrashAssistantViewController

This is the "landing" screen of the Crash Assistant feature. This will be presented first, than the `CrashAssistantChecklistViewController` above it. Right now it happens all the time (as requested), but it can be set to be shown via the `CrashAssistantViewController` initializer.

Regarding hierarchy, each indented element below represents a child of the element above it. The `CrashAssistantViewController` elements are divided from each other, with each element serving a different purpose.

```swift
// Title: Collect Crash Info
// Landing screen of the Crash Assist
// High level hierarchy overview

- CrashAssistantViewController: UIViewController
    - CrashAssistCategoryTableView: UIView
        - tableView: UITableView
            - [[CrashAssistCategoryCell: CustomViewCell]]
```

The `CrashAssistantViewController` creates the `CrashAssistCategoryTableView` and pins it to its `contentView`. The delegate

```swift
// CrashAssistantViewController.swift

override func viewDidLoad() {
    (...)
    let categoryTableView = CrashAssistCategoryTableView(
        delegate: self, 
        viewModel: viewModel)
    categoryTableView.pin(to: contentView)
}
```

As the `CrashAssistantViewController` is the view that holds everything together, it needs to handle some "heavy lifting." Therefore, a `delegate` is sent to the `CrashAssistCategoryTableView` to signal back to the `CrashAssistantViewController` when an event occurs using the following function:

```swift
func didSelect(section: Int)
```

In this particular case, the `tableView` will notify the `CrashAssistantViewController` about a cell selection, which will lead to the presentation of a new screen based on the `viewModel` that is used (which will be discussed in more detail in the [ViewModels](https://chat.openai.com/#viewmodels) section). The `viewModel` itself contains information about the `views` and the `data` that require representation. The presentable `viewController` will be the one that is set in the `viewModel` as a `type`. Since only `viewControllers` can present screens, it is not the `CrashAssistCategoryTableView`'s responsibility to create the new `viewController`. This is why the delegate function is necessary.

```swift
extension CrashAssistantViewController : CrashAssistCategoryTableViewDelegate {
    func didSelect(section: Int) {
        (...)
        let vc = selectedViewModel.viewControllerType.init(
            viewModel: selectedViewModel,
            crashIdData: viewModel?.crashIdData,
            delegate: self)
        let nav = UINavigationController(rootViewController: vc)

        present(nav, animated: true)
        (...)
    }
}
```

### CrashAssistantModalViewController

This `viewController` handles both the `Other Driver's info` and `Your info` screens.

### CrashAssistantInjuryViewController

### Views

### TableViews

### ViewModels

### Datas

### Protocols

### Delegates